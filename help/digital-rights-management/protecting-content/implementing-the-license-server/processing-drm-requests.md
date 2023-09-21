---
title: Processar solicitações do Adobe Primetime DRM
description: Processar solicitações do Adobe Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# Processar solicitações do Adobe Primetime DRM {#process-adobe-primetime-drm-requests}

A abordagem geral para gerenciar solicitações é criar um manipulador, analisar a solicitação, definir os dados de resposta ou o código de erro e fechar o manipulador.

A classe base usada para lidar com uma única interação de solicitação/resposta é `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Uma instância do `HandlerConfiguration` é usada para inicializar o manipulador. `HandlerConfiguration` armazena informações de configuração do servidor, incluindo credenciais de transporte, tolerância de carimbo de data e hora, listas de atualização de política e listas de revogação. O manipulador lê os dados da solicitação e analisa a solicitação em uma instância de `RequestMessageBase`. O chamador pode examinar as informações na solicitação e decidir se retorna um erro ou uma resposta bem-sucedida (subclasses de `RequestMessageBase` forneça um método para definir os dados de resposta).

Se a solicitação for bem-sucedida, defina os dados de resposta; caso contrário, chame `RequestMessageBase.setErrorData()` em caso de falha. Sempre encerre a implementação invocando o `close()` (recomenda-se que `close()` ser chamado no `finally` bloco de um `try` declaração). Consulte a `MessageHandlerBase` Documentação de referência de API para obter um exemplo de como chamar o manipulador.

>[!NOTE]
>
>O código de status HTTP 200 (OK) deve ser enviado em resposta a todas as solicitações processadas pelo manipulador. Se o manipulador não pôde ser criado devido a um erro do servidor, o servidor pode responder com outro código de status, como 500 (Erro interno do servidor).

O cliente usa o URL do License Server especificado no momento do empacotamento como o URL base para todas as solicitações enviadas ao servidor de licenças. Por exemplo, se o URL do servidor for especificado como &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, o cliente enviará solicitações para &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/.]> Consulte as seções a seguir para obter detalhes sobre o caminho específico usado para cada tipo de solicitação. Ao implementar seu servidor de licenças, certifique-se de que o servidor responde aos caminhos necessários para cada tipo de solicitação.

Uma solicitação de licença pode conter um token de autenticação. Se uma autenticação de nome de usuário/senha foi usada, a solicitação pode conter uma `AuthenticationToken` gerado pelo `AuthenticationHandler`, e o SDK garantirá que o token seja válido antes de emitir uma licença.

## Usar identificadores de máquina {#use-machine-identifiers}

Todas as solicitações do Adobe Primetime DRM (com exceção das solicitações que oferecem suporte à compatibilidade do FMRMS) incluem informações sobre o token do computador emitido para o cliente durante a individualização. O token do computador inclui uma ID de computador, que é um identificador atribuído durante a individualização. Você pode usar esse identificador para contar o número de computadores dos quais um usuário solicitou uma licença ou ingressou em um domínio.

Você pode usar um identificador da seguinte maneira:

* A variável `getUniqueId()` O método retorna uma string que foi atribuída a um dispositivo durante a individualização. Você pode armazenar as cadeias de caracteres em um banco de dados e pesquisar por identificador. No entanto, esse identificador será alterado se o usuário reformatar o disco rígido e individualizar novamente. Esse identificador também tem um valor diferente entre o Adobe AIR Adobe e o Flash Player em navegadores diferentes na mesma máquina.
* Se quiser contar as máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista antes, obtenha todos os identificadores para um nome de usuário e chame `matches()` para verificar se há correspondência. Como a variável `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`No entanto, essa opção só é prática quando há um pequeno número de valores para comparar; por exemplo, as máquinas associadas a um usuário específico.

## Autenticação do usuário {#user-authentication}

Uma solicitação DRM do Adobe Primetime pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha foi usada, a solicitação pode incluir um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Se quiser acessar e verificar o token, é necessário usar `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o `DRMManager.authenticate()` API do ActionScript ou iOS.

Se o cliente e o servidor usarem um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de algum outro canal e definirá o token de autenticação personalizado usando o `DRMManager.setAuthenticationToken` API do ActionScript 3.0. Uso `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor determina se o token de autenticação personalizado é válido.

## Proteção contra repetição {#replay-protection}

Para proteção contra repetição, verifique se o identificador de mensagem foi visto recentemente, chamando `RequestMessageBase.getMessageId()`. Nesse caso, um invasor pode estar tentando repetir a solicitação, que deve ser negada. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de IDs de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar o tempo que os identificadores de mensagem precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que carregue um carimbo de data e hora por mais do que o número especificado de segundos fora do horário do servidor.

## Detecção de reversão {#rollback-detection}

Para a detecção de reversão, algumas regras de uso exigem que o cliente mantenha informações de estado para aplicar os direitos. Por exemplo, para impor a regra de uso da janela de reprodução, o cliente armazena a data e a hora em que o usuário começou a visualizar o conteúdo pela primeira vez. Esse evento aciona o início da janela de reprodução. Para impor com segurança a janela de reprodução, o servidor precisa garantir que o usuário não esteja fazendo backup e restaurando o estado do cliente para remover a hora de início da janela de reprodução armazenada no cliente. O servidor faz isso rastreando o valor do contador de reversão do cliente.

Para cada solicitação, o servidor obtém o valor do contador chamando `RequestMessageBase.getClientState()` para obter a `ClientState` objeto e, em seguida, chamando `ClientState.getCounter()` para obter o valor atual do contador de estado do cliente. O servidor deve armazenar esse valor para cada cliente (use `MachineId.getUniqueId()` para identificar o cliente associado ao valor do contador de reversão) e, em seguida, chame `ClientState.incrementCounter()` para aumentar o valor do contador em um. Se o servidor detectar que o valor do contador é menor que o último valor visto pelo servidor, o estado do cliente pode ter sido revertido.

Consulte a `ClientState` Documentação de referência de API para obter mais informações sobre a detecção de violação do estado do cliente.

## Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando um `ServerConfigData` classe e chamada `HandlerConfiguration.setServerConfigData()`. Estas configurações aplicam-se somente às licenças emitidas por este servidor de licenças.

A tolerância do retrocesso do relógio é uma propriedade que pode ser definida pelo servidor de licenças para controlar como o cliente impõe licenças. Por padrão, os usuários podem atrasar o relógio da máquina 4 horas sem invalidar as licenças. Se um operador de servidor de licenças desejar usar uma configuração diferente, o novo valor poderá ser definido na variável `ServerConfigData` classe. Ao alterar o valor de qualquer uma dessas configurações, certifique-se de incrementar o número da versão chamando `setVersion()`. Os novos valores só serão enviados ao cliente se a versão no cliente for anterior à atual `ServerConfigData` versão.

## Arquivo de política DRM entre domínios {#crossdomain-drm-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política DRM entre domínios ( [!DNL crossdomain.xml]) é necessária para habilitar o SWF para solicitar licenças de um servidor de licenças. Um arquivo de política DRM entre domínios é representado por um arquivo XML que permite ao servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF servidos de outros domínios. Qualquer arquivo de SWF veiculado em um domínio especificado no arquivo de política DRM entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

A Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo somente que domínios confiáveis acessem o servidor de licença e limitando o acesso ao subdiretório de licença no servidor da Web.

Para obter mais informações sobre arquivos de política DRM entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política DRM)
* Especificação de arquivo de política DRM entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
