---
title: Guia do iOS/tvOS
description: Guia do iOS/tvOS
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Guia do SDK do iOS/tvOS {#iostvos-sdk-cookbook}

- [Introdução](#intro)
- [Fluxos de direito](#entitlement)
- [Informações relacionadas](#related)

>[!NOTE]
>
>**Aviso**: O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>


## Introdução {#intro}

Este documento descreve os workflows de direito que um aplicativo de nível superior do Programador pode implementar por meio das APIs expostas pela biblioteca iOS/tvOS AccessEnabler.

 

A solução de direito de autenticação da Adobe Primetime para iOS/tvOS é dividida em dois domínios:

- O domínio da interface do usuário: essa é a camada de aplicativo de nível superior que implementa a interface do usuário e usa os serviços fornecidos pela biblioteca AccessEnabler para fornecer acesso a conteúdo restrito.
- O domínio AccessEnabler - é aqui que os workflows de direito são implementados no formato de:
   - Chamadas de rede feitas para servidores backend do Adobe
   - Regras de lógica de negócios relacionadas aos workflows de autenticação e autorização
   - Gerenciamento de vários recursos e processamento do estado do workflow (como o cache de tokens)

O objetivo do domínio AccessEnabler é ocultar todas as complexidades dos workflows de direito e fornecer ao aplicativo de camada superior (por meio da biblioteca AccessEnabler) um conjunto de primitivos de direito simples com os quais você implementa os workflows de direito:

1. Definir a identidade do solicitante
1. Verificar e obter autenticação em relação a um determinado provedor de identidade
1. Verificar e obter autorização para um recurso específico
1. Logout
1. O Apple SSO flui por proxy na estrutura do Apple VSA

A atividade de rede do AccessEnabler ocorre em seu próprio thread, portanto, o thread da interface do usuário nunca é bloqueado. Como resultado, o canal de comunicação bidirecional entre os dois domínios de aplicativos deve seguir um padrão totalmente assíncrono:

- A camada do aplicativo da interface do usuário envia mensagens para o domínio AccessEnabler por meio das chamadas de API expostas pela biblioteca AccessEnabler .
- O AccessEnabler responde à camada da interface do usuário por meio dos métodos de retorno de chamada incluídos no protocolo AccessEnabler, que a camada da interface do usuário registra na biblioteca AccessEnabler .

 

## Configurar a ID do visitante {#visitorIDSetup}

Configurar uma [Marketing Cloud visitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) é muito importante do ponto de vista analítico. Depois que um valor visitorID é definido, o SDK envia essas informações juntamente com todas as chamadas de rede e o servidor de autenticação da Adobe Primetime coletará essas informações. No futuro, você poderá correlacionar a análise do serviço de Autenticação da Adobe Primetime com quaisquer outros relatórios do Analytics que você possa ter de outros aplicativos ou sites. Informações sobre como configurar a visitorID podem ser encontradas [here](#setOptions).

 

## Fluxos de direito {#entitlement}

A.  [Pré-requisitos](#prereqs) </br>
B.  [Fluxo de inicialização](#startup_flow) </br>
C.  [Fluxo de autenticação com Apple SSO](#authn_flow_wo_applesso)  </br>
D.  [Fluxo de autenticação com Apple SSO no iOS](#authn_flow_with_applesso) </br>
E.  [Fluxo de autenticação com Apple SSO no tvOS](#authn_flow_with_applesso_tvOS) </br>
F.  [Fluxo de autorização](#authz_flow) </br>
G.  [Exibir fluxo de mídia](#media_flow) </br>
H.  [Fluxo de logout sem Apple SSO](#logout_flow_wo_AppleSSO) </br>
I.  [Fluxo de logout com Apple SSO](#logout_flow_with_AppleSSO) </br>

 

### A. Pré-requisitos {#prereqs}

1. Crie suas funções de retorno de chamada:
   - `setRequestorComplete()` </br>
      - Disparado por [setRequestor()](#$setReq), retorna bem-sucedido ou falha. </br>
      - Sucesso indica que você pode continuar com chamadas de direito.
   - [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      - Disparado por [`getAuthentication()`](#$getAuthN) somente se o usuário não tiver selecionado um provedor (MVPD) e ainda não tiver sido autenticado. </br>
      - O `mvpds` é uma matriz de provedores disponíveis para o usuário.
   - `setAuthenticationStatus(status, errorcode)` </br>
      - Disparado por `checkAuthentication()` sempre.  </br>
      - Disparado por [`getAuthentication()`](#$getAuthN) somente se o usuário já estiver autenticado e tiver selecionado um provedor. </br>
      - O status retornado é bem-sucedido ou falha, o código de erro descreve o tipo da falha.
   - [`navigateToUrl(url)`](#$nav2url) </br>
      - Disparado por [`getAuthentication()`](#$getAuthN) depois que o usuário seleciona um MVPD.  O `url` fornece o local da página de logon do MVPD.
   - `sendTrackingData(event, data)` </br>
      - Disparado por `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.
      - O `event` parâmetro indica qual evento de direito ocorreu; o `data` é uma lista de valores relacionados ao evento. 
   - `setToken(token, resource)`

      - Disparado por [checkAuthorization()](#checkAuthZ) e [getAuthorization()](#$getAuthZ) após uma autorização bem-sucedida para visualizar um recurso.
      - O `token` é o token de mídia de curta duração; o `resource` é o conteúdo que o usuário está autorizado a visualizar.
   - `tokenRequestFailed(resource, code, description)` </br>
      - Disparado por [checkAuthorization()](#checkAuthZ) e [getAuthorization()](#$getAuthZ) após uma autorização infrutífera.
      - O `resource` é o conteúdo que o usuário estava tentando visualizar; o `code` é o código de erro que indica o tipo de falha ocorrido; o `description` descreve o erro associado ao código de erro.
   - `selectedProvider(mvpd)` </br>
      - Disparado por [`getSelectedProvider()`](#getSelProv).
      - O `mvpd` fornece informações sobre o provedor selecionado pelo usuário.
   - `setMetadataStatus(metadata, key, arguments)`
      - Disparado por `getMetadata().`
      - O `metadata` fornece os dados específicos solicitados; o
         `key` é a chave usada na variável [getMetadata()](#getMeta)
pedido; e 
`arguments` é o mesmo dicionário passado para [getMetadata()](#getMeta).
   - [&quot;preauthorizedResources(authorizedResources)`](#preauthResources)

      - Disparado por [`checkPreauthorizedResources()`](#checkPreauth).
      - O `authorizedResources` apresenta os recursos que o usuário está autorizado a visualizar.
   - [`currentTvProviderDialog(viewController)`](#presentTvDialog)
      - Disparado por [getAuthentication()](#getAuthN) quando o solicitante atual suporta pelo menos no MVPD que tenha suporte para SSO.
      - O parâmetro viewController é o Diálogo SSO do Apple e precisa ser apresentado no controlador de exibição principal.
   - [&quot;dismissTvProviderDialog(viewController)`](#dismissTvDialog)
      - Disparado por uma ação do usuário (selecionando &quot;Cancelar&quot; ou &quot;Outros provedores de TV&quot; na caixa de diálogo Apple SSO).
      - O parâmetro viewController é o Diálogo SSO do Apple e precisa ser descartado do controlador de visualização principal.












</br>


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOS_flows\(1\).png)\
 

### B. Fluxo de arranque {#startup_flow}

1. Inicie o aplicativo de nível superior.</br>
1. Iniciar autenticação da Adobe Primetime </br></br>
a. Chame [`init`](#$init) para criar uma única instância do AccessEnabler de autenticação da Adobe Primetime.
   - **Dependência:** Biblioteca nativa do iOS/tvOS de autenticação da Adobe Primetime (AccessEnabler)
   b. Chame `setRequestor()` Estabelecer a identidade do programador; passe no `requestorID` e (opcionalmente) uma matriz de endpoints de autenticação da Adobe Primetime. Para tvOS, você também precisará fornecer a chave pública e o segredo. Consulte [Documentação sem cliente](#create_dev) para obter detalhes.
   - **Dependência:** RequestorID de autenticação válida do Adobe Primetime\
      (Entre em contato com o Gerente de conta de autenticação da Adobe Primetime para fazer isso.)
   - **Acionadores:**

      [setRequestorComplete()](#$setReqComplete) callback
   >[!NOTE]
   >
   > **OBSERVAÇÃO:** Nenhum pedido de direito pode ser concluído até que a identidade do solicitante seja totalmente estabelecida. Isto significa, efetivamente, que [`setRequestor()`](#$setReq)  ainda estiver em execução, todas as solicitações de direito subsequentes (por exemplo, [`checkAuthentication()`](#checkAuthN) estão bloqueadas.

   Você tem duas opções de implementação: Depois que as informações de identificação do solicitante forem enviadas para o servidor de backend, a camada do aplicativo da interface do usuário poderá escolher uma das duas abordagens a seguir: </br>
   1. Aguarde o acionamento do [`setRequestorComplete()`](#setReqComplete) retorno de chamada (parte do delegado AccessEnabler).  Esta opção oferece a maior certeza de que [`setRequestor()`](#$setReq) concluído, portanto, é recomendado para a maioria das implementações.
   1. Continue sem esperar o acionamento da variável [`setRequestorComplete()`](#setReqComplete) retorno de chamada e início da emissão de solicitações de direito. Essas chamadas (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) são enfileiradas pela biblioteca AccessEnabler, que fará as chamadas de rede reais após a [`setRequestor()`](#$setReq). Ocasionalmente, essa opção pode ser interrompida se, por exemplo, a conexão de rede estiver instável.



1. Chame `checkAuthentication()` para verificar uma autenticação existente sem iniciar o fluxo de Autenticação completo.  Se esta chamada for bem-sucedida, você poderá prosseguir diretamente para o fluxo de Autorização.  Caso contrário, prossiga para o fluxo Autenticação .

   - **Dependência:** Uma chamada bem-sucedida para [setRequestor()](#$setReq)
(essa dependência também se aplica a todas as chamadas subsequentes).

   - **Acionadores:** [setAuthenticationStatus()](#$setAuthNStatus) callback

 

### C. Fluxo de autenticação sem Apple SSO {#authn_flow_wo_applesso}

1. Chame [`getAuthentication()`](#$getAuthN) para iniciar o fluxo de autenticação ou obter confirmação de que o usuário já está autenticado. \
   **Acionadores:**  

   - O [setAuthenticationStatus()](#$setAuthNStatus) retorno de chamada, se o usuário já estiver autenticado.  Nesse caso, prossiga diretamente para o [Fluxo de autorização](#authz_flow).
   - O [displayProviderDialog()](#$dispProvDialog) retorno de chamada, se o usuário ainda não estiver autenticado.  

1. Apresentar ao usuário a lista de provedores enviados para
   [`displayProviderDialog()`](#dispProvDialog).

1. Depois que o usuário selecionar um provedor, obtenha o URL do MVPD do usuário do `navigateToUrl:` ou `navigateToUrl:useSVC:` retorno de chamada e abra um `UIWebView/WKWebView` ou `SFSafariViewController` e direcione esse controlador para o URL.   

1. Por meio da `UIWebView/WKWebView` ou `SFSafariViewController` instanciado na etapa anterior, o usuário acessa a página de logon do MVPD e insere credenciais de logon. Várias operações de redirecionamento ocorrem dentro do controlador.</br></br>
   **OBSERVAÇÃO** - Nesse momento, o usuário tem a oportunidade de cancelar o fluxo de autenticação. Se isso ocorrer, a camada da interface do usuário será responsável por informar o AccessEnabler sobre esse evento, chamando [setSeletedProvider()](#setSelProv) com `null` como parâmetro. Isso permite que o AccessEnabler limpe seu estado interno e redefina o fluxo de autenticação.

1. Após um logon bem-sucedido pelo usuário, a camada do aplicativo detecta o carregamento de um URL personalizado específico. Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele deve ser interpretado somente pelo seu aplicativo como um sinal de que o fluxo de autenticação foi concluído e de que é seguro fechar o `UIWebView/WKWebView` ou `SFSafariViewController` controladora. No caso de um `SFSafariViewController `é necessário que o controlador seja usado, o URL personalizado específico é definido pela variável **`application's custom scheme`** (por exemplo,`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), caso contrário, esse URL personalizado específico será definido pela variável **`ADOBEPASS_REDIRECT_URL`** constante (ou seja, `adobepass://ios.app`).

1. Feche o controlador UIWebView/WKWebView ou SFSafariViewController e chame AccessEnabler `handleExternalURL:url `método da API`,` que instrui o AccessEnabler a recuperar o token de autenticação do servidor de back-end. 

1. [Opcional] Chame    [`checkPreauthorizedResources(resources)`](#$checkPreauth) para verificar quais recursos o usuário está autorizado a visualizar.  O `resources` é uma matriz de recursos protegidos associada ao token de autenticação do usuário.  Um uso para as informações de autorização obtidas do MVPD do usuário é decorar sua interface (por exemplo, símbolos bloqueados / desbloqueados ao lado do conteúdo protegido).

   - **Acionadores:** [`preauthorizedResources()`](#preauthResources) callback
   - **Ponto de execução:** Após o fluxo de autenticação concluído

1. Se a autenticação tiver sido bem-sucedida, prossiga para o Fluxo de autorização.

 

### D. Fluxo de autenticação com Apple SSO no iOS {#authn_flow_with_applesso}

1. Chame [`getAuthentication()`](#$getAuthN) para iniciar o fluxo de autenticação ou obter confirmação de que o usuário já está autenticado. \
   **Acionadores:**  

   - O [currentTvProviderDialog()](#presentTvDialog) retorno de chamada, se o usuário não estiver autenticado e o solicitante atual tiver pelo menos um MVPD compatível com SSO. Se nenhum MVPDs suportar SSO, o fluxo de autenticação clássico será usado.

1. Depois que o usuário seleciona um provedor, a biblioteca AccessEnabler obtém um token de autenticação com as informações fornecidas pela estrutura do VSA da Apple.

1. O [setAuthenticationsStatus()](#setAuthNStatus) o retorno de chamada será acionado. Nesse momento, o usuário deve ser autenticado com o Apple SSO.

1. [Opcional] Chame [`checkPreauthorizedResources(resources)`](#$checkPreauth) para verificar quais recursos o usuário está autorizado a visualizar. O `resources` é uma matriz de recursos protegidos associada ao token de autenticação do usuário.  Um uso para as informações de autorização obtidas do MVPD do usuário é decorar sua interface do usuário (por exemplo, símbolos bloqueados / desbloqueados ao lado do conteúdo protegido).

   - **Acionadores:** [`preauthorizedResources()`](#preauthResources) callback
   - **Ponto de execução:** Após o fluxo de autenticação concluído

1. Se a autenticação tiver sido bem-sucedida, prossiga para o Fluxo de autorização.

 

### E. Fluxo de autenticação com Apple SSO no tvOS {#authn_flow_with_applesso_tvOS}

1. Chame [`getAuthentication()`](#$getAuthN) para iniciar o fluxo de autenticação ou obter confirmação de que o usuário já está autenticado. \
   **Acionadores:**  
   - O [`presentTvProviderDialog()`](#presentTvDialog) retorno de chamada, se o usuário não estiver autenticado e o solicitante atual tiver pelo menos um MVPD compatível com SSO. Se nenhum MVPDs suportar SSO, o fluxo de autenticação clássico será usado.

1. Depois que o usuário seleciona um provedor, a variável [`status()`](#status_callback_implementation) o retorno de chamada será chamado. Um código de registro será fornecido e a biblioteca AccessEnabler começará a sondar o servidor para uma autenticação de segunda tela bem-sucedida.

1. Se o código de registro fornecido tiver sido usado para a autenticação bem-sucedida no segundo ecrã, a variável [`setAuthenticatiosStatus()`](#setAuthNStatus) o retorno de chamada será acionado. Nesse momento, o usuário deve ser autenticado com o Apple SSO.
1. [Opcional] Chame [`checkPreauthorizedResources(resources)`](#$checkPreauth) para verificar quais recursos o usuário está autorizado a visualizar. O `resources` é uma matriz de recursos protegidos associada ao token de autenticação do usuário.  Um uso para as informações de autorização obtidas do MVPD do usuário é decorar sua interface do usuário (por exemplo, símbolos bloqueados / desbloqueados ao lado do conteúdo protegido).
   - **Acionadores:** [`preauthorizedResources()`](#preauthResources) callback
   - **Ponto de execução:** Após o fluxo de autenticação concluído
1. Se a autenticação tiver sido bem-sucedida, prossiga para o Fluxo de autorização.

 

### F. Fluxo de autorização {#authz_flow}

1. Chame [getAuthorization()](#$getAuthZ) para iniciar o fluxo de autorização.
   - **Dependência:** ResourceID(s) válido(s) acordado(s) com o(s) MVPD(s).
   - As IDs de recurso devem ser as mesmas usadas em qualquer outro dispositivo ou plataforma e serão as mesmas em todos os MVPDs. Para obter informações sobre IDs de recursos, consulte [Identificação de recursos protegidos](https://tve.helpdocsonline.com/4-2-2-3)

1. Validar autenticação e autorização.

   - Se a variável [getAuthorization()](#$getAuthZ) chamada bem-sucedida: O usuário tem tokens AuthN e AuthZ válidos (o usuário é autenticado e autorizado a assistir a mídia solicitada).
   - If [getAuthorization()](#$getAuthZ) falha: Examine a exceção lançada para determinar seu tipo (AuthN, AuthZ ou algo diferente):
      - Se foi um erro de autenticação (AuthN), reinicie o fluxo de autenticação.
      - Se foi um erro de autorização (AuthZ), o usuário não está autorizado a assistir à mídia solicitada e algum tipo de mensagem de erro deve ser exibida para o usuário.
      - Se houver algum outro tipo de erro (erro de conexão, erro de rede etc.) em seguida, exibir uma mensagem de erro apropriada para o usuário.

1. Validar o token de mídia curta.\
   Use a biblioteca do Verificador de token de mídia de autenticação do Adobe Primetime para verificar o token de mídia de curta duração retornado do [getAuthorization()](#$getAuthZ) acima:

   - Se a validação tiver êxito: Reproduzir a mídia solicitada para o usuário.
   - Se a validação falhar: O token AuthZ era inválido, a solicitação de mídia deve ser recusada e uma mensagem de erro deve ser exibida ao usuário.


1. Retorne ao fluxo normal do aplicativo.

 

### G. Exibir fluxo de mídia {#media_flow}

1. O usuário seleciona a mídia a ser exibida.
1. A mídia está protegida?  O aplicativo verifica se a mídia selecionada está protegida:
   - Se a mídia selecionada estiver protegida, o aplicativo iniciará o [Fluxo de autorização](#authz_flow) acima.
   - Se a mídia selecionada não estiver protegida, reproduza a mídia para o usuário.

 

### H. Fluxo de logout sem Apple SSO {#logout_flow_wo_AppleSSO}

1. Chame [`logout()`](#$logout) para fazer logoff do usuário. O AccessEnabler limpa todos os valores e tokens em cache. Após limpar o cache, o AccessEnabler faz uma chamada de servidor para limpar as sessões do lado do servidor. Observe que, como a chamada do servidor pode resultar em um redirecionamento de SAML para IdP (isso permite a limpeza da sessão no lado do IdP), essa chamada deve seguir todos os redirecionamentos. Por esse motivo, essa chamada deve ser tratada em um controlador UIWebView/WKWebView ou SFSafariViewController.

   - a. Seguindo o mesmo padrão do workflow de autenticação, o domínio AccessEnabler faz uma solicitação para a camada do aplicativo da interface do usuário, por meio da `navigateToUrl:` ou `navigateToUrl:useSVC:` retorno de chamada, para criar um controlador UIWebView/WKWebView ou SFSafariViewController e instruir isso para carregar o URL fornecido no `url` parâmetro. Esse é o URL do endpoint de logout no servidor de back-end.

   - b. Seu aplicativo deve monitorar a atividade do `UIWebView/WKWebView or SFSafariViewController` e detectar o momento em que carrega um URL personalizado específico, já que ele passa por vários redirecionamentos. Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele só deve ser interpretado pelo seu aplicativo como um sinal de que o fluxo de logout foi concluído e de que é seguro fechar o `UIWebView/WKWebView` ou `SFSafariViewController` controladora. Quando o controlador carrega esse URL personalizado específico, seu aplicativo deve fechar o `UIWebView/WKWebView or SFSafariViewController` controlador e chame AccessEnabler `handleExternalURL:url`Método da API. No caso de um `SFSafariViewController`é necessário que o controlador seja usado, o URL personalizado específico é definido pela variável **`application's custom scheme`** (por exemplo, `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), caso contrário, esse URL personalizado específico será definido pela variável **`ADOBEPASS_REDIRECT_URL`**  constante (ou seja, `adobepass://ios.app`).

      >[!NOTE]
      >
      > **OBSERVAÇÃO:** O fluxo de logout é diferente do fluxo de autenticação, pois o usuário não precisa interagir com UIWebView/WKWebView ou SFSafariViewController de qualquer maneira. A camada de aplicativo da interface do usuário usa um UIWebView/WKWebView ou SFSafariViewController para garantir que todos os redirecionamentos estejam sendo seguidos. Portanto, é possível (e recomendado) tornar o controlador invisível (ou seja, oculto) durante o processo de logout.


### I. Fluxo de logout com Apple SSO {#logout_flow_with_AppleSSO}

1. Chame [`logout()`](#$logout) para fazer logoff do usuário. 
1. O [status()](#status_callback_implementation) o retorno de chamada será chamado com id VSA203.
1. O usuário também deve ser instruído a fazer logon a partir das configurações do sistema. Se isso não for feito, haverá uma reautenticação quando o aplicativo for reiniciado.

</br>

### Informações relacionadas {#related}

<!---
- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note) ](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->
