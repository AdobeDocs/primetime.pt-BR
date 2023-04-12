---
title: Referência da API do SDK do JavaScript
description: Referência da API do SDK do JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# Referência da API do SDK do JavaScript {#javascript-sdk-api-reference}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Referência da API {#api-reference}

Essas funções iniciam solicitações de interação com um MVPD. Todas as chamadas são assíncronas; é necessário implementar [retornos de chamada](#callbacks) para lidar com as respostas:

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSeletedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor (inRequestorID, endpoints, opções){#setrequestor(inRequestorID,endpoints,options)}

**Descrição:** Identifica o site de onde as solicitações se originam.  Você deve fazer essa chamada antes de qualquer outra chamada de API em uma sessão de comunicação. 

**Parâmetros:**

- *inRequestorID* - O identificador único atribuído ao Adobe do local de origem durante o registro.

- *endpoints* - Esse parâmetro é opcional. Pode ser um dos seguintes valores:

   - Uma matriz que permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (diferentes instâncias podem ser usadas para fins de depuração). Caso sejam fornecidos vários URLs, a lista MVPD é composta pelos pontos de extremidade de todos os provedores de serviços. Cada MVPD está associado ao prestador de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que suporta esse MVPD. Por padrão (se nenhum valor for especificado), o provedor de serviços da Adobe é usado (<http://sp.auth.adobe.com/>).

   Exemplo:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *opções* - Um objeto JSON contendo o valor da ID do aplicativo, as configurações sem atualização do valor da ID do visitante (logout do logon em segundo plano) e as configurações de MVPD (iFrame). Todos os valores são opcionais.
   1. Se especificado, a Experience Cloud visitorID será relatada em todas as chamadas de rede executadas pela biblioteca . O valor pode ser usado posteriormente para relatórios de análise avançados.
   2. Se o identificador exclusivo do aplicativo for especificado -`applicationId` - o valor será adicionado a todas as chamadas subsequentes feitas pelo aplicativo como parte do cabeçalho HTTP X-Device-Info . Esse valor pode ser buscado posteriormente de [ESM](/help/authentication/entitlement-service-monitoring-overview.md) relatórios que usam a consulta apropriada.

   **Observação:** Todas as chaves JSON fazem distinção entre maiúsculas e minúsculas.

    Exemplo:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- O Programador pode substituir as configurações do MVPD definidas na autenticação do Adobe Primetime, especificando se um iFrame é necessário ou não para logon (*iFrameRequired* chave) e as dimensões do iFrame (*iFrameWidth* e *iFrameHeight* chaves). O objeto JSON tem o seguinte modelo:

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```
 

Todas as chaves de nível superior no modelo acima são opcionais e têm valores padrão (*backgroundLogin*, *backgroundLogut* são falsas por padrão, e mvpdConfig é nulo (o que significa que nenhuma configuração de MVPD é substituída).

 
- **Observação**: A especificação de valores/tipos inválidos para os parâmetros acima resultará em um comportamento indefinido.

 

Veja um exemplo de configuração para o seguinte cenário: ativando o logon e o logout sem atualização, alterando o MVPD1 para o login de redirecionamento de página completo (não iFrame) e o MVPD2 para o login do iFrame com width=500 e height=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**Retornos de chamada acionados:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[Voltar para o início](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**Descrição:** Solicita autorização para o recurso especificado. Cada vez que um cliente tenta acessar um recurso autorizável, chame essa função para obter um token de autorização de duração curta do Criador de acesso. Os IDs dos recursos são acordados com o MVPD que fornece a autorização.

Usa o token de autenticação em cache para o cliente atual. Se esse token não for encontrado, inicia o processo de autenticação primeiro e continua com a autorização.\
 
**Parâmetros:**

- `inResourceID` - A ID do recurso para o qual o usuário solicita autorização.
- `redirect_url` - Opcionalmente, forneça um URL de redirecionamento, para que o processo de autorização do MVPD retorne o usuário para essa página, em vez da página da qual a autorização foi iniciada.


**Retornos de chamada acionados:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) sobre o sucesso, [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) em caso de falha

>[!CAUTION]
>
>Use checkAuthorization() em vez de getAuthorization() sempre que possível. O método getAuthorization() iniciará um fluxo de autenticação completo (se o usuário não estiver autenticado) e isso pode levar a uma implementação complicada no lado do Programador.

</b>

[Voltar para o início](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**Descrição:** Solicita autenticação para o cliente atual. Normalmente chamado em resposta a um clique em um botão de logon. Verifica se há um token de autenticação em cache para o cliente atual. Se esse token não for encontrado, o iniciará o processo de autenticação. Isso chama a caixa de diálogo de seleção de provedor padrão ou personalizada e usa o provedor selecionado para redirecionar para a interface de logon do MVPD.

Após o sucesso, o cria e armazena um token de autenticação para o usuário. Se a autenticação falhar, o provedor retornará uma mensagem de erro apropriada para sua [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) retorno de chamada.

**Parâmetros:**

- redirect_url - Como opção, forneça um URL de redirecionamento, para que o processo de autenticação do MVPD retorne o usuário para essa página, em vez da página a partir da qual a autenticação foi iniciada.

 **Retornos de chamada acionados:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Voltar para o início](#top)

</br>

## checkAuthN {#checkauthn}

**Descrição:** Verifica o status de autenticação atual do cliente atual.  Não associado a qualquer interface do usuário.

**Retornos de chamada acionados:** [setAuthentationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[Voltar para o início](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**Descrição:** Esse método é usado pelo aplicativo para verificar o status de autorização do cliente atual e do recurso em questão. Ele é iniciado verificando primeiro o status de autenticação. Se não estiver autenticado, o retorno de chamada tokenRequestFailed() será acionado e o método será encerrado. Se o usuário estiver autenticado, ele também acionará o fluxo de autorização. Veja os detalhes da [getAuthorization()](#getAuthZ método.

>[!TIP]
>
> **Uso de funções de status de verificação**  Você não precisa verificar o status de autenticação ou autorização antes de solicitar autorização. Você pode chamar essas funções, por exemplo, para atualizar sua própria exibição de status. Não os utilize quando necessitar de qualquer interação com o utilizador.

**Parâmetros:**

- `inResourceID` - A ID do recurso para o qual o usuário solicita autorização.

 
**Retornos de chamada acionados:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**Descrição:** Solicita o estatuto de autorização de &quot;comprovação&quot; para uma lista de recursos.

**Parâmetros:**

- *recursos*: O parâmetro resources é uma matriz de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID do recurso está sujeita às mesmas limitações que a ID do recurso na `getAuthorization()` ou seja, é um valor acordado estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia. 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

Essa variante da API está disponível a partir do JS SDK versão 4.0


**Parâmetros:**

- *recursos*: O parâmetro resources é uma matriz de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID do recurso está sujeita às mesmas limitações que a ID do recurso na `getAuthorization()` ou seja, é um valor acordado estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia. 

- *cache*: Use o cache interno ao verificar recursos pré-autorizados. Este é um parâmetro opcional, com o padrão de **true**. Se true, o comportamento será idêntico à API acima, o que significa que as chamadas subsequentes para essa função usarão um cache interno para resolver o recurso pré-autorizado. Passagem **false** para esse parâmetro, o desativará o cache interno, resultando em uma chamada de servidor sempre que a variável **checkPreauthorizedResources** A API é chamada.

**Retornos de chamada acionados:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[Voltar para o início](#top)
</br>

## getMetadata(Key) {#getMetadata}

**Descrição:** Recupera informações expostas como metadados pela biblioteca do Ativador de acesso.

Há dois tipos de metadados: 

- **Estático** (TTL do token de autenticação, TTL do token de autorização e ID do dispositivo) 
- **Metadados do usuário** (Inclui informações específicas do usuário transmitidas do MVPD para o dispositivo do usuário durante os fluxos de Autenticação e/ou Autorização)

**Mais informações:** [Metadados do usuário](#UserMetadata)

**Parâmetros:**

- *key*: Uma id que especifica os metadados solicitados:
   - Se a chave for `"TTL_AUTHN",` em seguida, o query é feito para obter o tempo de expiração do token de autenticação.

   - Se a chave for `"TTL_AUTHZ"` e params é uma matriz que contém a id do recurso como uma string, então a query é feita para obter a hora de expiração do token de autorização associado ao recurso especificado.

   - Se a chave for `"DEVICEID"` em seguida, o query é feito para obter a id do dispositivo atual. Observe que esse recurso está desativado por padrão e os programadores devem entrar em contato com o Adobe para obter informações sobre ativação e tarifas.

   - Se a chave for da seguinte lista de tipos de metadados de usuário, um objeto JSON contendo os metadados de usuário correspondentes será enviado para a [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) função de retorno de chamada:

   - `"zip"` - CEP

   - `"encryptedZip"` - CEP criptografado

   - `"householdID"` - Identificador da família. No caso em que um MVPD não suporta subcontas, isso será idêntico ao userID.

   - `"maxRating"` - Classificação parental máxima para o usuário

   - `"userID"` - O identificador do usuário. No caso em que um MVPD suporta subcontas e o usuário não é a conta principal, userID será diferente de householdID.

   - `"channelID"` - A lista de canais que o usuário tem direito a visualizar

   - `"is_hoh"` - Sinalizador que identifica se um usuário é chefe de família

   - `"encryptedZip"` - CEP criptografado

   - `"typeID"` - Sinalizador que identifica se a conta de usuário é primária/secundária

   - `"primaryOID"` - Identificador familiar

   - `"postalCode"` - Semelhante ao código postal

   - `"acctID"` - ID da conta

   - `"acctParentID"` - ID pai da conta
   **Observação**: Os metadados de usuário reais disponíveis para um Programador dependem do que um MVPD disponibiliza.  Consulte [Metadados do usuário](#UserMetadata) para a lista atual de metadados de usuário disponíveis.


Por exemplo:

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```
 

**Retornos de chamada acionados:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[Voltar para o início](#top)

</br>


## setSeletedProvider(providerid) {#setSelectedProvider}

**Descrição:** Chame esta função quando o usuário tiver selecionado um MVPD de sua interface de seleção de provedor para enviar a seleção de provedor para o Enabler de Acesso ou chame essa função com um parâmetro nulo caso o usuário tenha desconsiderado sua interface de seleção de provedor sem selecionar um provedor. 

**Retornos de chamada acionados:**[ setAuthentationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Voltar para o início](#top)

</br>

## getSeletedProvider() {#getSelectedProvider}

**Descrição:** Recupera os resultados da seleção do cliente na caixa de diálogo de seleção do provedor. Isso pode ser usado a qualquer momento após a verificação de autenticação inicial.

Essa função é assíncrona e retorna seu resultado para `selectedProvider()` função de retorno de chamada.

- **MVPD** O MVPD atualmente selecionado ou nulo se nenhum MVPD tiver sido selecionado.
- **AE_State** O resultado da autenticação para o cliente atual de &quot;Novo usuário&quot;, &quot;Usuário não autenticado&quot; ou &quot;Usuário autenticado&quot;

 **Retornos de chamada acionados:** [seletedProvider()](#getselectedprovider-getselectedprovider)

</br>

[Voltar para o início](#top)

</br>

## logout {#logout}

**Descrição:** Faz logoff do cliente atual, limpando todas as informações de autenticação e autorização desse usuário. Exclui todos os tokens authN e authZ do sistema do cliente.

 **Retornos de chamada acionados:** [setAuthentationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[Voltar para o início](#top)

</br>

## Definição de retorno de chamada {#calllback-definitions}

Você deve implementar esses retornos de chamada para lidar com as respostas às suas chamadas de solicitação assíncrona:

- [rightLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [seletedProvider()](#selectedproviderresult-selectedprovider)

</br>

## rightLoaded() {#entitlementLoaded}

**Descrição:** Disparado quando o Ativador de Acesso concluiu a inicialização e está pronto para receber solicitações. Implemente essa chamada de retorno para saber quando você pode iniciar a comunicação com a API do habilitador de acesso.
</br>

[Voltar ao início](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**Descrição:** Implemente este retorno de chamada para receber as informações de configuração e a lista MVPD.

**Parâmetros:**

- *configXML*: objeto xml contendo a configuração do REQUESTOR atual, incluindo a lista MVPD.

 
**Disparado por:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[Voltar ao início](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**Descrição:** Implemente esta chamada de retorno para invocar sua própria interface de usuário de seleção de provedor personalizada. Sua caixa de diálogo deve usar o nome de exibição (e o logotipo opcional) para fornecer as opções do cliente. Quando o cliente tiver feito uma escolha e descartado a caixa de diálogo, envie a ID associada para o provedor escolhido na chamada para o *setSeletedProvider()*.

**Parâmetros:**

- *provedores* - Uma matriz de objetos que representa os MVPDs solicitados:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**Disparado por:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[Voltar ao início](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**Descrição:** Implemente esse retorno de chamada se o usuário tiver selecionado um MVPD que exija um iFrame no qual será exibida a interface da página de logon de autenticação.

**Disparado por:**[ setSeletedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [Voltar ao início](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**Descrição:** Implemente esta chamada de retorno para receber o status de autenticação (1=autenticado ou 0=não autenticado) e uma mensagem de erro descritiva se ocorrer algum erro ao tentar determinar o status de autenticação (sequência vazia ao concluir com êxito a verificação).

>[!NOTE]
> 
>Se você estiver usando o [Relatório de erros avançados](/help/authentication/error-reporting.md) , você pode ignorar o parâmetro errorCode enviado para essa função.  No entanto, os sinalizadores isAuthenticated ainda são usados para rastrear o status de autenticação de um usuário no fluxo de direito


**Parâmetros:**

- *isAuthenticated* - Fornece o status de autenticação: 1 (autenticado) ou 0 (não autenticado).
- *errorCode* - Qualquer erro que ocorreu ao determinar o status de autenticação. Uma string vazia, se não houver.

 
**Disparado por:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[Voltar ao início](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>O tipo de dispositivo e o sistema operacional são derivados por meio do uso de uma biblioteca Java pública (<http://java.net/projects/user-agent-utils>) e a sequência do agente do usuário. Esteja ciente de que essas informações são fornecidas apenas como uma maneira abrangente de detalhar métricas operacionais em categorias de dispositivos, mas o Adobe não pode se responsabilizar por resultados incorretos. Use a nova funcionalidade adequadamente.

**Descrição:** Implemente essa chamada de retorno para receber dados de rastreamento quando eventos específicos ocorrerem. Você pode usar isso, por exemplo, para rastrear quantos usuários fizeram logon com as mesmas credenciais. No momento, o rastreamento não é configurável. Com a autenticação 1.6 da Adobe Primetime, `sendTrackingData()` além disso, relata informações sobre o dispositivo, o cliente Access Enabler e o tipo de sistema operacional. O `sendTrackingData()` o retorno de chamada permanece compatível com versões anteriores.\
 
- Valores possíveis para o tipo de dispositivo:
   - computador
   - tablet
   - dispositivo móvel
   - gameconsole
   - unknown

- Valores possíveis para o tipo de cliente Access Enabler:
   - html5
   - ios
   - android


Passa o tipo de evento e uma matriz de informações associadas. Os tipos de evento são:

| mvpdSelection | O usuário selecionou um MVPD em uma caixa de diálogo de seleção de provedor. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | Uma verificação de autenticação foi concluída. |
| authorizationDetection | Uma solicitação de autorização está concluída. |

</br>
Os dados são específicos para cada tipo de evento:
</br>

| Tipo de evento (String) | Dados (Matriz) |
|:--- | :--- |
| mvpdSelection | 0: MVPD selecionado |
|  | 1: Tipo de dispositivo |
|  | 2: Tipo de cliente Ativador de Acesso |
|  | 3: SO |
| authenticationDetection | 0: Se a solicitação de token foi bem-sucedida (true/false) |
|  | 1: ID do MVPD |
|  | 2: GUID |
|  | 3: Token já em cache (true/false) |
|  | 4: Tipo de dispositivo |
|  | 5: Tipo de cliente Ativador de Acesso |
|  | 6: SO |
| authorizationDetection | 0: Se a solicitação de token foi bem-sucedida (true/false) |
|  | 1: ID do MVPD |
|  | 2: GUID |
|  | 3: Token já em cache (true/false) |
|  | 4: Erro |
|  | 5: Detalhes |
|  | 6: Tipo de dispositivo |
|  | 7: Tipo de cliente Ativador de Acesso |
|  | 8: SO |


**Disparado por:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[Voltar ao início](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**Descrição:** Implemente esta chamada de retorno para receber o token de mídia de duração curta (inToken) e a ID do recurso (inRequestedResourceID) para o qual uma solicitação de autorização ou uma solicitação de autorização de verificação foi feita e foi concluída com êxito.

**Disparado por:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[Voltar ao início](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**Descrição:** Implemente esta chamada de retorno a ser sinalizada quando uma autorização ou um pedido de verificação falhar. Pode, opcionalmente, ser usado por um MVPD para fornecer uma mensagem personalizada a ser exibida pelo Programador.

>[!IMPORTANT]
>
>Essa função de retorno de chamada faz parte do antigo sistema de relatório de erros de autenticação do Primetime. Ele é retido para compatibilidade com versões anteriores, mas não é necessário usar essa função se você tiver implementado seus próprios retornos de chamada usando o sistema atual de Relatório de erros avançado. O sistema de relatório de erros mais recente fornece informações mais detalhadas sobre por que uma autorização (ou outra operação) falhou, juntamente com os cursos de ação sugeridos para cada tipo de erro ou aviso.

**Parâmetros:**

- *inRequestedResourceID* - Uma string que fornece o ID do recurso usado na solicitação de autorização.
- *inRequestErrorCode* - Uma string que exibe o código de erro de autenticação do Adobe Primetime, indicando o motivo da falha; Os valores possíveis são &quot;Erro de Usuário Não Autenticado&quot; e &quot;Erro de Usuário Não Autorizado&quot;; para obter mais detalhes, consulte &quot;Códigos de erro de chamada de retorno&quot; abaixo.
- *inRequestDetailedErrorMessage* - Uma string descritiva adicional adequada para exibição. Se essa string descritiva não estiver disponível por qualquer motivo, a autenticação da Adobe Primetime envia uma string vazia **(&quot;&quot;)**.  Isso pode ser usado por um MVPD para passar mensagens de erro personalizadas ou mensagens relacionadas a vendas. Por exemplo, se uma autorização para um recurso for negada a um assinante, o MVPD poderá responder com um `*inRequestDetailedErrorMessage*` como: **&quot;No momento, você não tem acesso a esse canal no seu pacote. Se quiser atualizar seu pacote, clique em \*aqui\*.&quot;** A mensagem é passada pela autenticação da Adobe Primetime por meio dessa chamada de retorno para o site do Programador. O Programador tem a opção de exibi-lo ou ignorá-lo. A autenticação da Adobe Primetime também pode usar `*inRequestDetailedErrorMessage*` para notificar o Programador da condição que pode ter levado a um erro. Por exemplo, **&quot;Ocorreu um erro de rede ao comunicar com o serviço de autorização do fornecedor&quot;.**

 

**Disparado por:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[Voltar ao início](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**Descrição:** Retorno acionado pelo Ativador de Acesso que entrega a lista de recursos autorizados retornada após uma chamada para `checkPreauthorizedResources()`.

**Parâmetros:**

- *authorizedResources*: A lista de recursos autorizados.

**Disparado por:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[Voltar ao início](#top)

</br>

## setMetadataStatus(chave, criptografada, dados) {#setMetadataStatus(key,encrypted,data)}

**Descrição:** Retorno de chamada acionado pelo Ativador de acesso que fornece os metadados solicitados por meio de um `getMetadata()` chame.

**Mais informações:** [Metadados do usuário](#userMetadata)

**Parâmetros:**

- *key (String)*: A chave dos metadados para os quais a solicitação foi feita.
- *criptografado (booleano)*: Um sinalizador que significa se o &quot;valor&quot; está criptografado ou não. Se isso for &quot;true&quot;, o &quot;valor&quot; será, na verdade, uma representação JSON Web Encrypted do valor real. 
- *dados (Objeto JSON)*: Um Objeto JSON com a representação dos metadados.Para solicitações simples (&#39;`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;), o resultado é uma String (representando o TTL de autenticação, o TTL de autorização ou a ID do dispositivo). No caso de uma solicitação de Metadados do usuário, o resultado pode ser um objeto primitivo ou JSON que representa a carga útil dos metadados. A estrutura real dos objetos de metadados do usuário JSON é semelhante ao seguinte:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```
 

Por exemplo:

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```
 

**Disparado por:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[Voltar ao início](#top)

</br>

## seletedProvider(result) {#selectedProvider(result)}

**Descrição:** Implemente este retorno de chamada para receber o MVPD selecionado no momento e o resultado da autenticação do usuário atual envolvido no `result` parâmetro. O `result` é um Object com as seguintes propriedades:

- **MVPD** O MVPD atualmente selecionado ou nulo se nenhum MVPD tiver sido selecionado.
- **AE\_State** O resultado da autenticação para o usuário atual, um de &quot;Novo usuário&quot;, &quot;Usuário não autenticado&quot; ou &quot;Usuário autenticado

 **Disparado por:** [getSeletedProvider()](#getSelProv)

</br>

[Voltar ao início](#top)

</br>

### Códigos de erro de chamada de retorno {#callback-error-codes}

| Erros genéricos |  |
|:--- | :--- | 
| Erro interno | Ocorreu um erro de sistema ao tentar processar a solicitação. |
| Erro do Provedor não Selecionado | Ocorre quando o cliente é cancelado na caixa de diálogo de seleção do provedor |
| Erro de Provedor Não Disponível | Ocorre quando nenhum provedor está disponível. |

| Erros de autenticação |  |
|:--- | :--- | 
| Erro de Autenticação Genérica | Retornado quando o motivo não é conhecido ou não pode ser publicado. |
| Erro de Autenticação Interna | Ocorreu um erro de sistema ao tentar autenticar. |
| Erro de Usuário Não Autenticado | O usuário não está autenticado. |
| Erro de várias solicitações de autenticação | Solicitações de autenticação adicionais foram recebidas antes da primeira conclusão. |

| Erros de autorização |  |
|:--- | :--- | 
| Erro de Autorização Genérica | Retornado quando o motivo não é conhecido ou não pode ser publicado. |
| Erro de Autorização Interna | Ocorreu um erro de sistema ao tentar autorizar. |
| Erro de Usuário não Autorizado | O cliente não está autorizado a visualizar o conteúdo solicitado. |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[Voltar para o início](#top)

