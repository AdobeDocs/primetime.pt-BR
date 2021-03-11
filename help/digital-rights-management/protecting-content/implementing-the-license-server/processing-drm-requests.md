---
title: Processar solicitações Adobe Primetime DRM
description: Processar solicitações Adobe Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# Processar solicitações Adobe Primetime DRM {#process-adobe-primetime-drm-requests}

A abordagem geral para gerenciar solicitações é criar um manipulador, analisar a solicitação, definir os dados de resposta ou o código de erro e fechar o manipulador.

A classe base usada para lidar com interação de solicitação/resposta única é `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Uma instância da classe `HandlerConfiguration` é usada para inicializar o manipulador. `HandlerConfiguration` armazena informações de configuração do servidor, incluindo credenciais de transporte, tolerância ao carimbo de data e hora, listas de atualização de política e listas de revogação. O manipulador lê os dados da solicitação e analisa a solicitação em uma instância de  `RequestMessageBase`. O chamador pode examinar as informações na solicitação e decidir se retorna um erro ou uma resposta bem-sucedida (as subclasses de `RequestMessageBase` fornecem um método para definir os dados de resposta).

Se a solicitação for bem-sucedida, defina os dados de resposta; caso contrário, chame `RequestMessageBase.setErrorData()` sobre falha. Encerre sempre a implementação chamando o método `close()` (recomenda-se que `close()` seja chamado no bloco `finally` de uma instrução `try`). Consulte a documentação de referência da API `MessageHandlerBase` para obter um exemplo de como chamar o manipulador.

>[!NOTE]
>
>O código de status HTTP 200 (OK) deve ser enviado em resposta a todas as solicitações processadas pelo manipulador. Se o manipulador não puder ser criado devido a um erro de servidor, o servidor poderá responder com outro código de status, como 500 (Internal Server Error).

O cliente usa o URL do License Server especificado no momento do empacotamento como o URL base para todas as solicitações enviadas para o servidor de licenças. Por exemplo, se o URL do servidor for especificado como &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, o cliente enviará solicitações para &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...] Consulte as seções a seguir para obter detalhes sobre o caminho específico usado para cada tipo de solicitação. Ao implementar o servidor de licenças, verifique se ele responde aos caminhos necessários para cada tipo de solicitação.

Uma solicitação de licença pode conter um token de autenticação. Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá conter um `AuthenticationToken` gerado pelo `AuthenticationHandler`, e o SDK garantirá que o token seja válido antes de emitir uma licença.

## Usar identificadores de máquina {#use-machine-identifiers}

Todas as solicitações de DRM da Adobe Primetime (com exceção das solicitações que oferecem suporte à compatibilidade com o FMRMS) incluem informações sobre o token do computador que foi emitido para o cliente durante a individualização. O token da máquina inclui uma ID da máquina, que é um identificador que foi atribuído durante a individualização. Você pode usar esse identificador para contar o número de máquinas das quais um usuário solicitou uma licença ou ingressou em um domínio.

Você pode usar um identificador da seguinte maneira:

* O método `getUniqueId()` retorna uma string que foi atribuída a um dispositivo durante a individualização. Você pode armazenar as cadeias de caracteres em um banco de dados e pesquisar por identificador. No entanto, esse identificador é alterado se o usuário reformata o disco rígido e se individualiza novamente. Esse identificador também tem um valor diferente entre o Adobe AIR e o Flash Player de Adobe em navegadores diferentes na mesma máquina.
* Se quiser contar máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista anteriormente, obtenha todos os identificadores de um nome de usuário e chame `matches()` para verificar se há correspondência. Como o método `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`, essa opção só é prática quando há um pequeno número de valores para comparar; por exemplo, as máquinas associadas a um usuário específico.

## Autenticação do usuário {#user-authentication}

Uma solicitação de DRM da Adobe Primetime pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha foi usada, a solicitação pode incluir um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Se quiser acessar e verificar o token, é necessário usar `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o ActionScript `DRMManager.authenticate()` ou a API do iOS.

Se o cliente e o servidor usarem um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de outro canal e definirá o token de autenticação personalizado usando a API `DRMManager.setAuthenticationToken` ActionScript 3.0. Use `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor determina se o token de autenticação personalizado é válido.

## Reproduzir proteção {#replay-protection}

Para proteção de repetição, você pode verificar se o identificador de mensagem foi visto recentemente, chamando `RequestMessageBase.getMessageId()`. Em caso afirmativo, um atacante pode estar a tentar responder novamente ao pedido, o que deve ser negado. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de ids de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar a quantidade de tempo em que os identificadores de mensagem precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que tenha um carimbo de data e hora por mais do que o número especificado de segundos da hora do servidor.

## Detecção de reversão {#rollback-detection}

Para detecção de reversão, algumas regras de uso exigem que o cliente mantenha as informações de estado para a aplicação dos direitos. Por exemplo, para impor a regra de uso da janela de reprodução, o cliente armazena a data e a hora em que o usuário começou a visualizar o conteúdo pela primeira vez. Esse evento aciona o início da janela de reprodução. Para aplicar com segurança a janela de reprodução, o servidor precisa garantir que o usuário não esteja fazendo backup e restaurando o estado do cliente para remover o tempo de início da janela de reprodução armazenado no cliente. O servidor faz isso rastreando o valor do contador de reversão do cliente.

Para cada solicitação, o servidor obtém o valor do contador ao chamar `RequestMessageBase.getClientState()` para obter o objeto `ClientState` e, em seguida, chamar `ClientState.getCounter()` para obter o valor atual do contador de estado do cliente. O servidor deve armazenar esse valor para cada cliente (use `MachineId.getUniqueId()` para identificar o cliente associado ao valor do contador de reversão) e, em seguida, chame `ClientState.incrementCounter()` para aumentar o valor do contador em um. Se o servidor detectar que o valor do contador é inferior ao último valor visto pelo servidor, o estado do cliente pode ter sido revertido.

Consulte a documentação de referência da API `ClientState` para obter mais informações sobre a detecção de adulteração do estado do cliente.

## Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando uma classe `ServerConfigData` e chamando `HandlerConfiguration.setServerConfigData()`. Essas configurações se aplicam somente às licenças emitidas por este servidor de licenças.

A tolerância de retorno de chamada do relógio é uma propriedade que pode ser definida pelo servidor de licença para controlar como o cliente aplica licenças. Por padrão, os usuários podem retornar o relógio da máquina 4 horas sem invalidar licenças. Se um operador de servidor de licenças quiser usar uma configuração diferente, o novo valor poderá ser definido na classe `ServerConfigData`. Ao alterar o valor de qualquer uma dessas configurações, incremente o número da versão chamando `setVersion()`. Os novos valores só serão enviados para o cliente se a versão no cliente for anterior à versão atual `ServerConfigData`.

## Arquivo de política DRM entre domínios {#crossdomain-drm-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política de DRM entre domínios ( [!DNL crossdomain.xml]) será necessário para habilitar o SWF para solicitar licenças de um servidor de licença. Um arquivo de política de DRM entre domínios é representado por um arquivo XML que permite ao servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF enviados de outros domínios. Qualquer arquivo SWF servido de um domínio especificado no arquivo de política DRM entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

O Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo que apenas domínios confiáveis acessem o servidor de licenças e limitando o acesso ao subdiretório de licenças no servidor da Web.

Para obter mais informações sobre arquivos de política de DRM entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política DRM)
* Especificação do arquivo de política de DRM entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)