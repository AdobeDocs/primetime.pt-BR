---
seo-title: Processar solicitações Adobe Primetime DRM
title: Processar solicitações Adobe Primetime DRM
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# Processar solicitações Adobe Primetime DRM {#process-adobe-primetime-drm-requests}

A abordagem geral para gerenciar solicitações é criar um manipulador, analisar a solicitação, definir os dados de resposta ou o código de erro e fechar o manipulador.

A classe base usada para lidar com interação de solicitação única/resposta é `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Uma instância da `HandlerConfiguration` classe é usada para inicializar o manipulador. `HandlerConfiguration` armazena informações de configuração do servidor, incluindo credenciais de transporte, tolerância de carimbo de data e hora, listas de atualização de política e listas de revogação. O manipulador lê os dados da solicitação e analisa-a em uma instância do `RequestMessageBase`. O chamador pode examinar as informações na solicitação e decidir se deve retornar um erro ou uma resposta bem-sucedida (as subclasses de `RequestMessageBase` um método para definir os dados de resposta).

Se a solicitação for bem-sucedida, defina os dados da resposta; caso contrário, invoque `RequestMessageBase.setErrorData()` em falha. Sempre encerre a implementação chamando o `close()` método (recomenda-se que `close()` seja chamado no `finally` bloco de uma `try` instrução). Consulte a documentação de referência da `MessageHandlerBase` API para obter um exemplo de como chamar o manipulador.

>[!NOTE]
>
>O código de status HTTP 200 (OK) deve ser enviado em resposta a todas as solicitações processadas pelo manipulador. Se o manipulador não puder ser criado devido a um erro de servidor, o servidor poderá responder com outro código de status, como 500 (Internal Server Error).

O cliente usa o URL do License Server especificado no momento da empacotamento como o URL base para todas as solicitações enviadas ao servidor de licenças. Por exemplo, se o URL do servidor for especificado como &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, o cliente enviará solicitações para &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> Consulte as seções a seguir para obter detalhes sobre o caminho específico usado para cada tipo de solicitação. Ao implementar o servidor de licenças, verifique se ele responde aos caminhos necessários para cada tipo de solicitação.

Uma solicitação de licença pode conter um token de autenticação. Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá conter um `AuthenticationToken` gerado pelo `AuthenticationHandler`SDK, e ele garantirá que o token seja válido antes de emitir uma licença.

## Usar identificadores de máquina {#use-machine-identifiers}

Todas as solicitações do Adobe Primetime DRM (com exceção das solicitações que oferecem suporte à compatibilidade do FMRMS) incluem informações sobre o token do computador que foi emitido para o cliente durante a individualização. O token de máquina inclui uma ID de máquina, que é um identificador que foi atribuído durante a individualização. Você pode usar esse identificador para contar o número de computadores dos quais um usuário solicitou uma licença ou ingressou em um domínio.

Você pode usar um identificador da seguinte maneira:

* O `getUniqueId()` método retorna uma string que foi atribuída a um dispositivo durante a individualização. É possível armazenar as strings em um banco de dados e pesquisar por identificador. No entanto, esse identificador muda se o usuário reformata o disco rígido e se individualiza novamente. Esse identificador também tem um valor diferente entre o Adobe AIR e o Flash Player Adobe em navegadores diferentes na mesma máquina.
* Se quiser contar máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista antes, obtenha todos os identificadores de um nome de usuário e chame `matches()` para verificar se há correspondência. Como o `matches()` método deve ser usado para comparar os valores retornados por `MachineId.getBytes`, essa opção só é prática quando há um pequeno número de valores a serem comparados; por exemplo, as máquinas associadas a um usuário específico.

## Autenticação do usuário {#user-authentication}

Uma solicitação do Adobe Primetime DRM pode conter um token de autenticação.

Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá incluir um `AuthenticationToken` gerado pelo `AuthenticationHandler`. Se quiser acessar e verificar o token, é necessário usá-lo `RequestMessageBase.getAuthenticationToken()`. Para iniciar uma solicitação de nome de usuário/senha no cliente, use o `DRMManager.authenticate()` ActionScript ou a API do iOS.

Se o cliente e o servidor usarem um mecanismo de autenticação personalizado, o cliente obterá um token de autenticação por meio de outro canal e definirá o token de autenticação personalizado usando a API do `DRMManager.setAuthenticationToken` ActionScript 3.0. Use `RequestMessageBase.getRawAuthenticationToken()` para obter o token de autenticação personalizado. A implementação do servidor determina se o token de autenticação personalizado é válido.

## Proteção contra repetição {#replay-protection}

Para obter proteção de reprodução, verifique se o identificador de mensagem foi visto recentemente, ligando para `RequestMessageBase.getMessageId()`. Em caso afirmativo, um atacante pode estar a tentar repetir o pedido, que deve ser negado. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de IDs de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar a quantidade de tempo que os identificadores de mensagens precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que tenha um carimbo de data e hora por mais do que o número especificado de segundos após o horário do servidor.

## Detecção de retorno {#rollback-detection}

Para a detecção de reversão, algumas regras de uso exigem que o cliente mantenha informações de estado para a aplicação dos direitos. Por exemplo, para impor a regra de uso da janela de reprodução, o cliente armazena a data e a hora em que o usuário começou a exibir o conteúdo pela primeira vez. Este evento aciona o start da janela de reprodução. Para aplicar com segurança a janela de reprodução, o servidor precisa garantir que o usuário não esteja fazendo backup e restaurando o estado do cliente para remover o tempo de start da janela de reprodução armazenado no cliente. O servidor faz isso rastreando o valor do contador de reversão do cliente.

Para cada solicitação, o servidor obtém o valor do contador chamando `RequestMessageBase.getClientState()` para obter o `ClientState` objeto e, em seguida, chamando `ClientState.getCounter()` para obter o valor atual do contador de estado do cliente. O servidor deve armazenar esse valor para cada cliente (use `MachineId.getUniqueId()` para identificar o cliente associado ao valor do contador de reversão) e, em seguida, chamar `ClientState.incrementCounter()` para aumentar o valor do contador em um. Se o servidor detectar que o valor do contador é menor que o último valor visto pelo servidor, o estado do cliente pode ter sido revertido.

Consulte a documentação de referência da `ClientState` API para obter mais informações sobre a detecção de adulteração do estado do cliente.

## Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando uma `ServerConfigData` classe e chamando `HandlerConfiguration.setServerConfigData()`. Essas configurações se aplicam somente às licenças emitidas por este servidor de licenças.

A tolerância de retorno de travamento do relógio é uma propriedade que pode ser definida pelo servidor de licenças para controlar como o cliente aplica licenças. Por padrão, os usuários podem retornar o relógio da máquina 4 horas sem invalidar licenças. Se um operador de servidor de licenças desejar usar uma configuração diferente, o novo valor poderá ser definido na `ServerConfigData` classe. Ao alterar o valor de qualquer uma dessas configurações, certifique-se de aumentar o número da versão chamando `setVersion()`. Os novos valores só serão enviados para o cliente se a versão no cliente for anterior à `ServerConfigData` versão atual.

## Arquivo de política DRM entre domínios {#crossdomain-drm-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política DRM entre domínios ( [!DNL crossdomain.xml]) será necessário para permitir que o SWF solicite licenças de um servidor de licença. Um arquivo de política DRM entre domínios é representado por um arquivo XML que permite ao servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF fornecidos de outros domínios. Qualquer arquivo SWF servido de um domínio especificado no arquivo de política DRM entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

A Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo apenas que domínios confiáveis acessem o servidor de licenças e limitando o acesso ao subdiretório de licenças no servidor Web.

Para obter mais informações sobre arquivos de política DRM entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política DRM)
* Especificação do arquivo de política DRM entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)