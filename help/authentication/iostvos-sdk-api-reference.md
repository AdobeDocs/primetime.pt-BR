---
title: Referência da API do iOS/tvOS
description: Referência da API do iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '7000'
ht-degree: 0%

---


# Referência da API do SDK do iOS/tvOS {#iostvos-sdk-api-reference}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#intro}

Esta página descreve os métodos e as funções de retorno de chamada expostos pelo cliente nativo do iOS/tvOS para autenticação da Adobe Primetime. Os métodos e as funções de retorno de chamada descritos aqui são definidos na variável `AccessEnabler.h` e `EntitlementDelegate.h` arquivos de cabeçalho; você pode encontrá-las no SDK do iOS AccessEnabler aqui: `[SDK directory]/AccessEnabler/headers/api/`


Documentação associada:

* Para obter uma descrição do fluxo básico de direito de autenticação do Primetime, consulte [Fluxo de direitos](/help/authentication/entitlement-flow.md).
* Para obter uma apresentação passo a passo de como implementar o fluxo de direito de autenticação do Primetime usando essa API, consulte o [Guia de integração do iOS](/help/authentication/iostvos-sdk-cookbook.md).
* Para obter o SDK do iOS AccessEnabler mais recente, consulte [Biblioteca iOS Native Access Enabler](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

>[!NOTE]
>
>O Adobe incentiva você a usar somente a autenticação do Primetime *público* APIs:
>
>* As APIs públicas estão disponíveis e são totalmente testadas em todos os tipos de clientes compatíveis. Para qualquer recurso público, garantimos que cada tipo de cliente tenha uma versão correspondente do(s) método(s) associado(s).
>* As APIs públicas devem ser o mais estáveis possível, para oferecer suporte à compatibilidade com versões anteriores e garantir que as integrações de parceiros não sejam interrompidas. No entanto, para APIs não públicas, reservamos o direito de alterar sua assinatura em qualquer ponto futuro. Se você encontrar um fluxo específico que não pode ser suportado por meio de uma combinação das chamadas públicas atuais da API de autenticação do Primetime, a melhor abordagem é nos informar. Levando em conta suas necessidades, podemos modificar as APIs públicas e fornecer uma solução estável a partir de agora.


</br>

## Referência da API {#apis}

* [init](#initWithSoftwareStatement):softwareStatement - Instancia o objeto AccessEnabler.

* **[OBSOLETO]** [init](#init) - Instancia o objeto AccessEnabler.

* [setOptions:options:](#setOptions) - Define opções globais do SDK, como profile ou visitorID.

* [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:serviceProviders:](#setReqV3) - Estabelece a identidade do Programador.

* **[OBSOLETO]** [setRequestor:signedRequestorId:](#setReq),[setRequestor:signedRequestorId:serviceProviders:](#setReq) - Estabelece a identidade do Programador.

* **[OBSOLETO]** [setRequestor:signedRequestorId:secret:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos)-Estabelece a identidade do Programador.

* [setRequestorComplete:](#setReqComplete) - Informa o aplicativo de que a fase de configuração está concluída.

* [checkAuthentication](#checkAuthN) - Verifica o status de autenticação do usuário atual.

* [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN) - Inicia o fluxo de trabalho de autenticação completo.

* [getAuthentication:filter](#getAuthN_filter),[getAuthentication:withData:](#getAuthN)[eFilter](#getAuthN_filter) - Inicia o fluxo de trabalho de autenticação completo.

* [displayProviderDialog:](#dispProvDialog) - Informa seu aplicativo para instanciar os elementos de interface apropriados para o usuário selecionar um MVPD.

* [setSeletedProvider:](#setSelProv) - Informa o AccessEnabler da seleção MVPD do usuário.

* [navigateToUrl:](#nav2url) - Informa seu aplicativo que o usuário precisa ser apresentado com a página de logon do MVPD.

* [navigateToUrl:useSVC:](#nav2urlSVC) - Informa seu aplicativo que o usuário precisa ser apresentado com a página de logon do MVPD, usando o SFSafariViewController

* [handleExternalURL:url](#handleExternalURL) - Conclui o fluxo de autenticação/logout.

* **[OBSOLETO]** [getAuthenticationToken](#getAuthNToken) - Solicita o token de autenticação do servidor de back-end.

* [setAuthenticationStatus:errorCode:](#setAuthNStatus) - Informa o aplicativo do status do fluxo de autenticação.

* [checkPreauthorizedResources:](#checkPreauth) - Determina se o usuário já está autorizado a visualizar recursos protegidos específicos.

* [checkPreauthorizedResources:cache:](#checkPreauthCache) - Determina se o usuário já está autorizado a visualizar recursos protegidos específicos.

* [PreauthorizedResources:](#preauthResources) - Fornece uma lista de recursos que o usuário já está autorizado a visualizar.

* [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ) - Verifica o status de autorização do usuário atual.

* [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ) - Inicia o fluxo de autorização.

* [setToken:forResource:](#setToken) - Informa o seu pedido de que o fluxo de autorização foi concluído com êxito.

* [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) - Informa o seu pedido de que o fluxo de autorização falhou.

* [logout](#logout) - Inicia o fluxo de logout.

* [getSeletedProvider](#getSelProv) - Determina o provedor selecionado no momento.

* [seletedProvider:](#selProv) - Fornece informações sobre o MVPD atualmente selecionado para seu aplicativo.

* [getMetadata:](#getMeta) - Recupera informações expostas como metadados pela biblioteca AccessEnabler.

* [currentTvProviderDialog:](#presentTvDialog) - Informa seu aplicativo a exibir a caixa de diálogo SSO do Apple.

* [dismissTvProviderDialog:](#dismissTvDialog) - Informa seu aplicativo a ocultar a caixa de diálogo SSO do Apple.

* [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus) - Fornece os metadados solicitados por um [getMetadata:](#getMeta) chame.

* [sendTrackingData:forEventType:](#sendTracking) - Fornece informações de dados de rastreamento.

* [MVPD](#mvpd) - A classe MVPD. [Contém informações sobre o MVPD]

### init:softwareStatement {#initWithSoftwareStatement}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Instancia o objeto AccessEnabler. Deve haver uma única instância AccessEnabler por instância de aplicativo.

| **Chamada da API: Construtor do iOS AccessEnabler** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**Disponibilidade:** v3.0+

**Parâmetros:**

* **softwareStatement:** Uma string que identifica o aplicativo no sistema Adobe. Veja como obter uma declaração de software.

[Voltar ao topo...](#apis)



### init - [OBSOLETO]{#init}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Instancia o objeto AccessEnabler. Deve haver uma única instância AccessEnabler por instância de aplicativo.

| Chamada da API: Construtor do iOS AccessEnabler |
| --- |
| ```- (id) init;``` |

**Disponibilidade:** v1.0+ **Até:** v3.0

**Parâmetros:** Nenhum

[Voltar ao topo...](#apis)

</br>

### setOptions:options {#setOptions}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Define opções globais do SDK. Aceita um NSDictionary como um argumento. Os valores do dicionário serão passados para o servidor, juntamente com todas as chamadas de rede feitas pelo SDK.

**Observação:** Os valores serão transmitidos ao servidor independentemente do fluxo atual (autenticação/autorização). Se quiser alterar os valores, você pode chamar esse método em qualquer momento.

| Chamada da API: setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**Disponibilidade:** v2.3.0+

**Parâmetros:**

* *opções*: Um NSDictionary contendo opções globais do SDK. Atualmente, as seguintes opções estão disponíveis:
   * **applicationProfile** - Ele pode ser usado para fazer configurações de servidor com base nesse valor.
   * **visitorID** - A visitorID do Marketing Cloud. Esse valor pode ser usado posteriormente em relatórios de análise avançados.
   * **handleSVC** - Booleano indicando se o programador lidará com os SFSafariViewControllers. Consulte [Suporte SFSafariViewController no iOS SDK 3.2+](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) para obter mais detalhes.
      * Se estiver definido como **false,** o SDK apresentará automaticamente ao usuário final um SFSafariViewController. O SDK navegará ainda mais para o URL da página de logon dos MVPDs.
      * Se estiver definido como **true,** o SDK **NOT** apresentar automaticamente ao usuário final um SFSafariViewController. O SDK acionará ainda mais **navigate(toUrl:{url}, useSVC:YES)**.
* **device\_info** - Informações sobre o cliente, conforme descrito em [Enviando informações do cliente](/help/authentication/passing-client-information-device-connection-and-application.md).

[Voltar ao topo...](#apis)


### setRequestor:requestorID, setRequestor:requestorID:serviceProviders: {#setReqV3}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Estabelece a identidade do Programador. Cada Programador recebe uma ID exclusiva ao se registrar no Adobe para o sistema de autenticação do Primetime. Ao lidar com o SSO e tokens remotos, o estado de autenticação pode mudar quando o aplicativo está em segundo plano, setRequestor pode ser chamado novamente quando o aplicativo é trazido para o primeiro plano para sincronizar com o estado do sistema (busque um token remoto se o SSO estiver ativado ou exclua o token local se um logout tiver ocorrido enquanto isso).

A resposta do servidor contém uma lista de MVPDs junto com algumas informações de configuração anexadas à identidade do Programador. A resposta do servidor é usada internamente pelo código AccessEnabler. Somente o status da operação (ou seja, SUCCESS/FAIL) é apresentado ao seu aplicativo por meio da variável `setRequestorComplete:` retorno de chamada.

Se a variável `urls` não for usado, a chamada de rede resultante será direcionada ao URL padrão do provedor de serviços: o ambiente Adobe VERSÃO/produção.


Se um valor for fornecido para a variável `urls` , a chamada de rede resultante é direcionada a todos os URLs fornecidos no `urls` parâmetro. Todas as solicitações de configuração são acionadas simultaneamente em threads separados. O primeiro entrevistado tem precedência ao compilar a lista de MVPDs. Para cada MVPD na lista, o AccessEnabler lembra o URL do provedor de serviços associado. Todas as solicitações de direito subsequentes são direcionadas para o URL associado ao provedor de serviços que foi emparelhado com o MVPD de destino durante a fase de configuração.

| Chamada da API: configuração do solicitante |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**Disponibilidade:** v3.0+

| Chamada da API: configuração do solicitante |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**Disponibilidade:** v3.0+

**Parâmetros:**

* *requestorID*: A ID exclusiva associada ao Programador. Passe a ID exclusiva atribuída pelo Adobe para o seu site ao se registrar pela primeira vez no serviço de autenticação do Primetime.
* *urls*: Parâmetro opcional; por padrão, o provedor de serviços da Adobe é usado (http://sp.auth.adobe.com/). Essa matriz permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (diferentes instâncias podem ser usadas para fins de depuração). Você pode usar isso para especificar várias instâncias do provedor de serviços de autenticação do Primetime. Ao fazer isso, a lista MVPD é composta pelos pontos de extremidade de todos os provedores de serviços. Cada MVPD está associado ao prestador de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que suporta esse MVPD.

>[!NOTE]
>
>Se chamado sem o `serviceProviders` , a biblioteca recuperará a configuração do provedor de serviços padrão (ou seja, `https://sp.auth.adobe.com` para o perfil de produção ou `https://sp.auth-staging.adobe.com` para o perfil de preparo). Se a variável `serviceProviders` for fornecido, deverá ser uma matriz de URLs. As informações de configuração são recuperadas de todos os pontos de extremidade especificados e são mescladas. Se houver informações duplicadas em diferentes respostas do provedor de serviços, o conflito será resolvido em favor do servidor que responder mais rápido (ou seja, o servidor com o menor tempo de resposta terá prioridade).

**Retornos de chamada acionados:** [`setRequestorComplete:`](#setReqComplete)

[Voltar ao topo...](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:serviceProviders: - [OBSOLETO] {#setReq}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Estabelece a identidade do Programador. Cada Programador recebe uma ID exclusiva ao se registrar no Adobe para o sistema de autenticação do Primetime. Ao lidar com o SSO e tokens remotos, o estado de autenticação pode mudar quando o aplicativo está em segundo plano, setRequestor pode ser chamado novamente quando o aplicativo é trazido para o primeiro plano para sincronizar com o estado do sistema (busque um token remoto se o SSO estiver ativado ou exclua o token local se um logout tiver ocorrido enquanto isso).

A resposta do servidor contém uma lista de MVPDs junto com algumas informações de configuração anexadas à identidade do Programador. A resposta do servidor é usada internamente pelo código AccessEnabler. Somente o status da operação (ou seja, SUCCESS/FAIL) é apresentado ao seu aplicativo por meio da variável `setRequestorComplete:` retorno de chamada.

Se a variável `urls` não for usado, a chamada de rede resultante será direcionada ao URL padrão do provedor de serviços: o ambiente Adobe VERSÃO/produção.

Se um valor for fornecido para a variável `urls` , a chamada de rede resultante é direcionada a todos os URLs fornecidos no `urls` parâmetro. Todas as solicitações de configuração são acionadas simultaneamente em threads separados. O primeiro entrevistado tem precedência ao compilar a lista de MVPDs. Para cada MVPD na lista, o AccessEnabler lembra o URL do provedor de serviços associado. Todas as solicitações de direito subsequentes são direcionadas para o URL associado ao provedor de serviços que foi emparelhado com o MVPD de destino durante a fase de configuração.

| Chamada da API: configuração do solicitante |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**Disponibilidade:** v1.0+ **Até:** v3.0

| Chamada da API: configuração do solicitante |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**Disponibilidade:** v1.0+ **Até:** v3.0

**Parâmetros:**

* *requestorID*: A ID exclusiva associada ao Programador. Passe a ID exclusiva atribuída pelo Adobe ao seu site quando se registrou pela primeira vez no serviço de autenticação do Primetime.
* *signedRequestorID*: **Esse parâmetro existe no iOS AccessEnabler versões 1.2 e posteriores.** Uma cópia da ID do solicitante que é assinada digitalmente com sua chave privada. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *urls*: Parâmetro opcional; por padrão, o provedor de serviços da Adobe é usado (http://sp.auth.adobe.com/). Essa matriz permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (diferentes instâncias podem ser usadas para fins de depuração). Você pode usar isso para especificar várias instâncias do provedor de serviços de autenticação do Primetime. Ao fazer isso, a lista MVPD é composta pelos pontos de extremidade de todos os provedores de serviços. Cada MVPD está associado ao prestador de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que suporta esse MVPD.

**Notas:** Se chamado sem o `serviceProviders` , a biblioteca recuperará a configuração do provedor de serviços padrão (ou seja,`https://sp.auth.adobe.com` para o perfil de produção ou `https://sp.auth-staging.adobe.com` para o perfil de preparo). Se a variável `serviceProviders` for fornecido, deverá ser uma matriz de URLs. As informações de configuração são recuperadas de todos os pontos de extremidade especificados e são mescladas. Se houver informações duplicadas em diferentes respostas do provedor de serviços, o conflito será resolvido em favor do servidor que responder mais rápido (ou seja, o servidor com o menor tempo de resposta terá prioridade).

**Retornos de chamada acionados:** [`setRequestorComplete:`](#setReqComplete)


[Voltar ao topo...](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey, setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [OBSOLETO] {#setReq_tvos}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Estabelece a identidade do Programador. Cada Programador recebe uma ID exclusiva ao se registrar no Adobe para o sistema de autenticação do Primetime. Essa configuração deve ser executada somente uma vez durante o ciclo de vida do aplicativo.

A resposta do servidor contém uma lista de MVPDs junto com algumas informações de configuração anexadas à identidade do Programador. A resposta do servidor é usada internamente pelo código AccessEnabler. Somente o status da operação (ou seja, SUCCESS/FAIL) é apresentado ao seu aplicativo por meio da variável `setRequestorComplete:` retorno de chamada.

Se a variável `urls` não for usado, a chamada de rede resultante será direcionada ao URL padrão do provedor de serviços: o ambiente Adobe VERSÃO/produção.

Se um valor for fornecido para a variável `urls` , a chamada de rede resultante é direcionada a todos os URLs fornecidos no `urls` parâmetro. Todas as solicitações de configuração são acionadas simultaneamente em threads separados. O primeiro entrevistado tem precedência ao compilar a lista de MVPDs. Para cada MVPD na lista, o AccessEnabler lembra o URL do provedor de serviços associado. Todas as solicitações de direito subsequentes são direcionadas para o URL associado ao provedor de serviços que foi emparelhado com o MVPD de destino durante a fase de configuração.



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: configuração do solicitante</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidade:** v2.0+ **Até:** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: configuração do solicitante</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v2.0+ **Até:** v3.0

**Parâmetros:**

* *requestorID*: A ID exclusiva associada ao Programador. Passe a ID exclusiva atribuída pelo Adobe ao seu site quando se registrou pela primeira vez no serviço de autenticação do Primetime.
* *signedRequestorID*: **Esse parâmetro existe no iOS AccessEnabler versões 1.2 e posteriores.** Uma cópia da ID do solicitante que é assinada digitalmente com sua chave privada. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *urls*: Parâmetro opcional; por padrão, o provedor de serviços da Adobe é usado (http://sp.auth.adobe.com/). Essa matriz permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (diferentes instâncias podem ser usadas para fins de depuração). Você pode usar isso para especificar várias instâncias do provedor de serviços de autenticação do Primetime. Ao fazer isso, a lista MVPD é composta pelos pontos de extremidade de todos os provedores de serviços. Cada MVPD está associado ao prestador de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que suporta esse MVPD.
* secret e publicKey: A chave secreta e pública usada para assinar as chamadas de segunda tela. Para obter mais informações, consulte [Documentação sem cliente](#create_dev).

Se chamado sem o `serviceProviders` , a biblioteca recuperará a configuração do provedor de serviços padrão (ou seja, `https://sp.auth.adobe.com` para o perfil de produção ou https://sp.auth-staging.adobe.com para o perfil de preparo). Se a variável `serviceProviders` for fornecido, deverá ser uma matriz de URLs. As informações de configuração são recuperadas de todos os pontos de extremidade especificados e são mescladas. Se houver informações duplicadas em diferentes respostas do provedor de serviços, o conflito será resolvido em favor do servidor que responder mais rápido (ou seja, o servidor com o menor tempo de resposta terá prioridade).

**Retornos de chamada acionados:** [`setRequestorComplete:`](#setReqComplete)

[Voltar ao topo...](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que informa ao aplicativo que a fase de configuração está concluída. Este é um sinal de que o aplicativo pode iniciar a emissão de solicitações de direito. Nenhum pedido de direito pode ser emitido pelo aplicativo até a fase de configuração ser concluída.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: configuração do solicitante concluída</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidade:** v1.0+

**Parâmetros**:

* *status*: pode assumir um dos seguintes valores:
   * `ACCESS_ENABLER_STATUS_SUCCESS` - a fase de configuração foi concluída com êxito
   * `ACCESS_ENABLER_STATUS_ERROR` - falha na fase de configuração

**Disparado por:**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[Voltar ao topo...](#apis)

</br>

### checkAuthentication {#checkAuthN}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Verifica o status de autenticação do usuário atual.
Ele faz isso procurando por um token de autenticação válido no espaço de armazenamento de token local. Chamar esse método não executa chamadas de rede. Ele é usado pelo aplicativo para consultar o status de autenticação do usuário e atualizar a interface do usuário adequadamente (ou seja, atualizar a interface de logon/logout). O status de autenticação é comunicado ao aplicativo por meio da variável [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) retorno de chamada.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: verificar status de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[Voltar ao topo...](#apis)

</br>

### getAuthentication, getAuthentication:withData: {#getAuthN}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Inicia o fluxo de trabalho de autenticação completo. Ele é iniciado verificando o status de autenticação. Se ainda não estiver autenticado, a máquina de estado do fluxo de autenticação será iniciada:

* se a última tentativa de autenticação tiver sido bem-sucedida, a fase de seleção do MVPD será ignorada e a variável [`navigateToUrl:`](#nav2url) o retorno de chamada é acionado. O aplicativo usa essa chamada de retorno para instanciar o controle WebView que apresenta ao usuário a página de logon do MVPD. **[OBSERVAÇÃO: A partir do Access Enabler 1.5, essa funcionalidade não está disponível devido a uma limitação no SDK].**
* se a última tentativa de autenticação não tiver sido bem-sucedida ou se o usuário tiver feito logout explicitamente, a variável [`displayProviderDialog:`](#dispProvDialog) o retorno de chamada é acionado. Seu aplicativo usa esse retorno de chamada para exibir a interface de seleção do MVPD. Além disso, seu aplicativo é necessário para retomar o fluxo de autenticação, informando a biblioteca do AccessEnabler sobre a seleção MVPD do usuário por meio do [`setSelectedProvider:`](#setSelProv) método .

À medida que as credenciais do usuário são verificadas na página de logon do MVPD, seu aplicativo é necessário para monitorar as várias operações de redirecionamento que ocorrem enquanto o usuário é autenticado na página de logon do MVPD. Quando as credenciais corretas são inseridas, o controle WebView é redirecionado para um URL personalizado definido pela variável `ADOBEPASS_REDIRECT_URL` constante. Esse URL não deve ser carregado pelo WebView. O aplicativo deve interceptar esse URL e interpretar esse evento como um sinal de que a fase de logon está concluída. Em seguida, ele deve entregar o controle para o AccessEnabler para concluir o fluxo de autenticação (chamando a função [handleExternalURL](#handleExternalURL) método ).

Por fim, o status de autenticação é comunicado ao aplicativo por meio da variável [setAuthenticationStatus:errorCode:](#setAuthNStatus) retorno de chamada.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: inicia o fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: inicia o fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Disponibilidade:** v1.9+

**Parâmetros:**

* *forceAuthn*: Um sinalizador que especifica se o fluxo de autenticação deve ser iniciado, independentemente de o usuário já estar autenticado ou não.
* *dados*: Um dicionário que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK.

**Retornos de chamada acionados:** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[Voltar ao topo...](#apis)

</br>

### getAuthentication:filter, getAuthentication:withData:eFilter {#getAuthN_filter}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Inicia o fluxo de trabalho de autenticação completo. Ele é iniciado verificando o status de autenticação. Se ainda não estiver autenticado, a máquina de estado do fluxo de autenticação será iniciada:

* [currentTvProviderDialog()](#presentTvDialog) será chamado se o solicitante atual tiver pelo menos um MVPD que seja compatível com SSO. Se nenhum MVPD suportar SSO, o fluxo de autenticação clássico começará e o parâmetro de filtro será ignorado.
* Depois que o usuário conclui o fluxo de SSO do Apple [dismissTvProviderDialog()](#dismissTvDialog) será acionado e o processo de autenticação será concluído.

Por fim, o status de autenticação é comunicado ao aplicativo por meio da variável [setAuthenticationStatus:errorCode:](#setAuthNStatus) retorno de chamada.

**Disponibilidade:** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: inicia o fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: inicia o fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parâmetros:**

* *forceAuthn*: Um sinalizador que especifica se o fluxo de autenticação deve ser iniciado, independentemente de o usuário já estar autenticado ou não.
* *dados*: Um dicionário que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK. 
* filtro: Um dicionário com duas listas de IDs MVPD que devem aparecer na caixa de diálogo SSO do Apple. Qualquer MVPD que não suporte SSO será ignorado, mas a ordem será respeitada. O dicionário precisa ter duas chaves:
   * TV\_PROVIDERS: Uma lista com todos os MVPDs que devem aparecer no seletor
   * FEATURED\_TV\_PROVIDERS: Uma lista com todos os MVPDs que devem ser marcados como exibidos no seletor. Os MVPDs nesta lista também devem ser especificados na lista TV\_PROVIDERS.

**Disponibilidade:** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: inicia o fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: inicia o fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parâmetros:**

* *forceAuthn*: Um sinalizador que especifica se o fluxo de autenticação deve ser iniciado, independentemente de o usuário já estar autenticado ou não.
* *dados*: Um dicionário que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK. 
* filtro: Uma lista de IDs MVPD que devem aparecer na caixa de diálogo SSO do Apple. Qualquer MVPD que não suporte SSO será ignorado, mas a ordem será respeitada.

**Retornos de chamada acionados:** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[Voltar ao topo...](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler para informar ao aplicativo que os elementos apropriados da interface do usuário precisam ser instanciados para permitir que o usuário selecione o MVPD desejado. O retorno de chamada fornece uma lista de objetos MVPD com informações adicionais que podem ajudar a criar corretamente o painel da interface de seleção (como o URL apontando para o logotipo do MVPD, nome de exibição amigável etc.)

Depois que o usuário seleciona o MVPD desejado, o aplicativo da camada superior é necessário para retomar o fluxo de autenticação chamando `setSelectedProvider:` e transmitindo a ID do MVPD correspondente à seleção do usuário.

**Abortar o fluxo de autenticação** - Este é um ponto em que o usuário tem a capacidade de pressionar o botão &quot;Voltar&quot;, o que equivale a abortar o fluxo de autenticação. Nesse cenário, o aplicativo deve chamar a função [setSeletedProvider:](#setSelProv) , passando null como parâmetro, para dar ao AccessEnabler a oportunidade de redefinir seu estado-máquina de autenticação.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: exibir a interface de seleção do MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidade:** v1.0+

**Parâmetros**:

* *mvpds*: lista de objetos MVPD contendo informações relacionadas ao MVPD que o aplicativo pode usar para criar os elementos da interface de seleção do MVPD.

**Disparado por:** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[Voltar ao topo...](#apis)

</br>

#### setSeletedProvider: {#setSelProv}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Este método é chamado pelo seu aplicativo para informar o Ativador de Acesso sobre a seleção MVPD do usuário. O aplicativo pode usar esse método para selecionar ou alterar o provedor de serviços usado para autenticação.

Se o MVPD selecionado for um MVPD TempPass, ele será autenticado automaticamente com esse MVPD sem precisar chamar getAuthentication() depois.

Observe que isso não é possível para o Pass de Temp Promocional, onde parâmetros extras são fornecidos no método getAuthentication() .

Ao passar *null* como parâmetro, o Access Enabler assume que o usuário cancelou o fluxo de autenticação (ou seja, pressionou o botão &quot;Voltar&quot;) e responde redefinindo a máquina de estado de autenticação e chamando a função [setAuthenticationStatus:errorCode:](#setAuthNStatus) retorno de chamada com o `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` código de erro.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: definir o provedor selecionado no momento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[Voltar ao topo...](#apis)

</br>

#### navigateToUrl: {#nav2url}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição:** Retorno de chamada acionado pelo AccessEnabler para solicitar que seu aplicativo instancie um controlador UIWebView/WKWebView e carregue o URL fornecido no **`url`** parâmetro. O retorno de chamada passa a variável **`url`** que representa o URL do endpoint de autenticação ou o URL do endpoint de logout.

Como UIWebView/WKWebView` `O controlador passa por vários redirecionamentos, seu aplicativo deve monitorar a atividade do controlador e detectar o momento em que ele carrega um URL personalizado específico definido pelo `ADOBEPASS_REDIRECT_URL `constante (ou seja, `adobepass://ios.app`). Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele só deve ser interpretado pelo seu aplicativo como um sinal de que o fluxo de autenticação ou logout foi concluído e de que é seguro fechar o controlador. Quando o controlador carrega esse URL personalizado específico, seu aplicativo deve fechar o UIWebView/WKWebView e chamar o `handleExternalURL:url `Método da API.

**Observação:** Observe que, no caso do fluxo de autenticação, esse é um ponto em que o usuário tem a capacidade de pressionar o botão &quot;Voltar&quot;, o que equivale à interrupção do fluxo de autenticação. Nesse cenário, o aplicativo é obrigado a chamar a função [setSeletedProvider:](#setSelProv) aprovação de método **`nil`** como o parâmetro e dando uma chance ao AccessEnabler para redefinir seu estado-máquina de autenticação.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: exibir página de logon MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros**:

* *url*: o URL apontando para a página de logon do MVPD

**Disparado por:** [setSeletedProvider:](#setSelProv)

 

[Voltar ao topo...](#apis)

</br>

#### navigateToUrl:useSVC: {#nav2urlSVC}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição:** Retorno acionado pelo AccessEnabler em vez do `navigateToUrl:` retorno de chamada caso seu aplicativo tenha habilitado anteriormente o controle do Safari View Controller (SVC) manual via [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) e somente no caso de MVPDs que exigem o Safari View Controller (SVC). Para todos os outros MVPDs, a variável `navigateToUrl:` o retorno de chamada será chamado. Consulte[Suporte SFSafariViewController no iOS SDK 3.2+](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) para obter detalhes sobre como o Safari View Controller (SVC) deve ser gerenciado.

Semelhante ao `navigateToUrl:` retorno de chamada `navigateToUrl:useSVC:` é acionado pelo AccessEnabler para solicitar que seu aplicativo instancie um `SFSafariViewController` e para carregar o URL fornecido no **`url`** parâmetro. O retorno de chamada passa a variável **`url`** que representa o URL do endpoint de autenticação ou o URL do endpoint de logout e o parâmetro **`useSVC`** que especifica que o aplicativo deve usar um `SFSafariViewController`.

Como `SFSafariViewController` O controlador passa por vários redirecionamentos, seu aplicativo deve monitorar a atividade do controlador e detectar o momento em que ele carrega um URL personalizado específico definido por seu `application's custom scheme` (por exemplo,** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`). Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele só deve ser interpretado pelo seu aplicativo como um sinal de que o fluxo de autenticação ou logout foi concluído e de que é seguro fechar o controlador. Quando o controlador carrega esse URL personalizado específico, seu aplicativo deve fechar o `SFSafariViewController` e faça uma chamada para AccessEnabler `handleExternalURL:url `Método da API.

**Observação:** Observe que, no caso do fluxo de autenticação, esse é um ponto em que o usuário tem a capacidade de pressionar o botão &quot;Voltar&quot;, o que equivale à interrupção do fluxo de autenticação. Nesse cenário, o aplicativo é obrigado a chamar a função [setSeletedProvider:](#setSelProv) aprovação de método **`nil`** como o parâmetro e dando uma chance ao AccessEnabler para redefinir seu estado-máquina de autenticação.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: exibir página de logon MVPD no SFSafariViewController</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:**v 3.2+

**Parâmetros**:

* *url:* o URL apontando para a página de logon do MVPD
* *useSVC:* se o url deve ser carregado no SFSafariViewController.

**Disparado por:**[ setOptions:](#setOptions) before [setSeletedProvider:](#setSelProv) 

[Voltar ao topo...](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Esse método é chamado pelo aplicativo para concluir o fluxo de autenticação ou logout. Esse método deve ser chamado logo após o aplicativo detectar o momento em que a função `UIWebView/WKWebView or SFSafariViewController` O controlador é redirecionado para um URL personalizado específico. Caso seu aplicativo seja necessário usar um `SFSafariViewController `controladora o URL personalizado específico é definido pelo seu `application's custom scheme` (por exemplo,`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), caso contrário, esse URL personalizado específico será definido pela variável `ADOBEPASS_REDIRECT_URL `constante (ou seja, `adobepass://ios.app`).

No caso do fluxo de autenticação, o AccessEnabler conclui o fluxo recuperando o token de autenticação do servidor de back-end e armazenando-o localmente no armazenamento do token. O AccessEnabler informará o aplicativo de que o fluxo de autenticação foi concluído, chamando a função `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> retorno de chamada com um código de status 1, indicando sucesso. Se houver um erro durante a execução dessas etapas, a variável `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> O retorno de chamada é acionado com um código de status de 0, indicando falha de autenticação, bem como um código de erro correspondente.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: concluir o fluxo de autenticação ou logout</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code> (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v3.0+

**Parâmetros:** 

* *url*: O URL interceptado do ` UIWebView/WKWebView or SFSafariViewController ` controle como string.


**Retornos de chamada acionados:** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[Voltar ao topo...](#apis)

</br>

#### getAuthenticationToken - [OBSOLETO] {#getAuthNToken}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Conclui o fluxo de autenticação solicitando o token de autenticação do servidor de back-end. Este método deve ser chamado pelo seu aplicativo somente em resposta a um evento em que o controle WebView que hospeda a página de logon MVPD é redirecionado para o URL personalizado definido pelo `ADOBEPASS_REDIRECT_URL` constante.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: recuperar o token de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+ **Até:** v3.0

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[Voltar ao topo...](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que informa o aplicativo sobre o status do fluxo de autenticação. Há muitos locais em que esse fluxo pode falhar, seja como resultado da interação do usuário ou devido a outros cenários imprevistos (ou seja, problemas de conectividade de rede etc.). Esse retorno de chamada informa o aplicativo sobre o status de sucesso/falha do fluxo de autenticação, fornecendo também informações adicionais sobre o motivo da falha, quando necessário.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: relatar o status do fluxo de autenticação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**Disponibilidade:** v1.0+

**Parâmetros**:

* *status*: pode assumir um dos seguintes valores:
   * `ACCESS_ENABLER_STATUS_SUCCESS` - o fluxo de autenticação foi concluído com êxito
   * `ACCESS_ENABLER_STATUS_ERROR` - falha no fluxo de autenticação
* *código*: motivo da falha. If *status* é `ACCESS_ENABLER_STATUS_SUCCESS`, em seguida *código* é uma string vazia (ou seja, definida pela variável `USER_AUTHENTICATED` constante). Em caso de falha, esse parâmetro pode assumir um dos seguintes valores:
   * `USER_NOT_AUTHENTICATED_ERROR` - O usuário não está autenticado. Em resposta à [checkAuthentication:](#checkAuthN) chamada de método quando não houver um token de autenticação válido no cache de token local.
   * `PROVIDER_NOT_SELECTED_ERROR` - O AccessEnabler redefiniu a máquina de estado de autenticação após a aprovação do aplicativo de camada superior *null* para [`setSelectedProvider:`](#setSelProv) para suspender o fluxo de autenticação.  Provavelmente, o usuário cancelou o fluxo de autenticação (ou seja, pressionou o botão &quot;Voltar&quot;).
   * `GENERIC_AUTHENTICATION_ERROR` - O fluxo de autenticação falhou devido a motivos como indisponibilidade da rede ou o usuário cancelou explicitamente o fluxo de autenticação.

**Disparado por:** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[Voltar ao topo...](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Esse método é usado pelo aplicativo para determinar se o usuário já está autorizado a visualizar recursos protegidos específicos. O objetivo principal desse método é recuperar informações para uso na decoração da interface do usuário **(por exemplo, indicando o status de acesso com ícones de bloqueio e desbloqueio).**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: definir o provedor selecionado no momento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.3+

**Parâmetros:**

* *recursos:* conjunto de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID de recurso está sujeita às mesmas limitações que a ID de recurso na chamada, ou seja, deve ser um valor acordado estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia.

**Retorno de chamada acionado:** [`preauthorizedResources:`](#preauthResources)

[Voltar ao topo...](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Esse método é usado pelo aplicativo para determinar se o usuário já está autorizado a visualizar recursos protegidos específicos. O objetivo principal desse método é recuperar informações para uso na decoração da interface do usuário (por exemplo, indicando o status de acesso com ícones de bloqueio e desbloqueio). O **cache** controla se o cache interno é usado para resolver recursos.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: definir o provedor selecionado no momento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilidade:** v3.1+

 

**Parâmetros:**

* *recursos:* conjunto de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID do recurso está sujeita às mesmas limitações que a ID do recurso na `getAuthorization:` ou seja, deve ser um valor acordado estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia.
* *cache:* Booleano especificando se o cache interno deve ser usado para resolver recursos. Se falso, o cache será ignorado, resultando em chamadas do servidor toda vez que essa API for chamada.

**Retorno de chamada acionado:** [`preauthorizedResources:`](#preauthResources)

[Voltar ao topo...](#apis)

</br>

### PreauthorizedResources: {#preauthResources}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição:** Retorno de chamada acionado por `checkPreauthorizedResources:`. Fornece uma lista de recursos que o usuário já está autorizado a visualizar.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: definir o provedor selecionado no momento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.3+

**Parâmetros:**

* `resources`: matriz de recursos para os quais o usuário já está autorizado a visualizar.

**Disparado por:** [`checkPreauthorizedResources:`](#checkPreauth)

 

[Voltar ao topo...](#apis)

</br>

### checkAuthorization:, checkAuthorization:withData: {#checkAuthZ}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Este método é usado pelo aplicativo para verificar o status da autorização. Ele é iniciado verificando primeiro o status de autenticação. Se não estiver autenticado, a variável [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) o retorno de chamada é acionado e o método sai. Se o usuário estiver autenticado, ele também acionará o fluxo de autorização. Veja os detalhes da [`getAuthorization:`](#getAuthZ) método .


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: verificar status de autorização</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: verificar status de autorização</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.9+

**Parâmetros:**

* *recurso*: a ID do recurso para o qual o usuário solicita autorização.
* *dados*: Um dicionário que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK. 

**Retornos de chamada acionados:**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[Voltar ao topo...](#apis)

</br>

### getAuthorization:, getAuthorization:withData: {#getAuthZ}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Este método é utilizado pelo pedido para iniciar o fluxo de autorização. Se o usuário ainda não estiver autenticado, ele também iniciará o fluxo de autenticação. Se o usuário for autenticado, o AccessEnabler continuará a emitir solicitações para o token de autorização (se nenhum token de autorização válido estiver presente no cache de token local) e para o token de mídia de curta duração. Quando o token de mídia curto for obtido, o fluxo de autorização será considerado concluído. O [setToken:forResource:](#setToken) o retorno de chamada é acionado e o token de mídia curto é entregue como parâmetro para o aplicativo. Se, por qualquer motivo, a autorização falhar, a variável [tokenRequestFailed:forEventType:](#tokenReqFailed) a chamada de retorno é acionada e o código/detalhes do erro são fornecidos.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: iniciar o fluxo de autorização</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: iniciar o fluxo de autorização</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilidade:** v1.9+

**Parâmetros:**

* *recurso*: a ID do recurso para o qual o usuário solicita autorização.
* *dados*: Um dicionário que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK. 

**Retornos de chamada acionados:** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**Retornos de chamada adicionais acionados:**\
Esse método também pode acionar os seguintes retornos de chamada (se o fluxo de autenticação também for iniciado): `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`\
 
**OBSERVAÇÃO: Use checkAuthorization: / checkAuthorization:withData: em vez de getAuthorization: / getAuthorization:withData: sempre que possível. A getAuthorization: / getAuthorization:withData: O método iniciará um fluxo de autenticação completo (se o usuário não estiver autenticado) e isso pode levar a uma implementação complicada no lado do Programador.**

[Voltar ao topo...](#apis)

</br>

### setToken:forResource: {#setToken}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que informa ao seu aplicativo que o fluxo de autorização foi concluído com êxito. O token de mídia de curta duração também é fornecido como parâmetro.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: fluxo de autorização concluído com êxito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros**:

* *token*: o token de mídia de curta duração
* *recurso*: o recurso para o qual foi obtida a autorização

**Disparado por:** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[Voltar ao topo...](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que informa ao aplicativo da camada superior que o fluxo de autorização falhou.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: falha no fluxo de autorização</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros**:

* *recurso*: O recurso para o qual a autorização foi obtida.
* *código*: O código de erro associado ao cenário de falha. Valores possíveis:
   * `USER_NOT_AUTHORIZED_ERROR` - o usuário não pôde autorizar para o recurso em questão
* *descrição*: Detalhes adicionais sobre o cenário de falha. Se essa string descritiva não estiver disponível por qualquer motivo, a autenticação do Primetime enviará uma string vazia **(&quot;&quot;)**. \
   Essa sequência de caracteres pode ser usada por um MVPD para passar mensagens de erro personalizadas ou mensagens relacionadas a vendas. Por exemplo, se uma autorização para um recurso for negada a um assinante, o MVPD poderá enviar uma mensagem como: &quot;No momento, você não tem acesso a esse canal no seu pacote. Se quiser atualizar seu pacote, clique em **here**.&quot; A mensagem é passada pela autenticação do Primetime por meio dessa chamada de retorno para o Programador, que tem a opção de exibi-la ou ignorá-la. A autenticação do Primetime também pode usar esse parâmetro para fornecer uma notificação da condição que pode ter levado a um erro. Por exemplo, &quot;Ocorreu um erro de rede ao comunicar com o serviço de autorização do fornecedor&quot;.

**Disparado por:** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[Voltar ao topo...](#apis)

</br>

### logout {#logout}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Esse método é chamado pelo seu aplicativo para iniciar o fluxo de logout. O logout é o resultado de uma série de operações de redirecionamento HTTP porque o usuário precisa ser desconectado dos servidores de Autenticação Primetime e também dos servidores MVPD. Como esse fluxo não pode ser concluído com uma simples solicitação HTTP emitida pela biblioteca do AccessEnabler, um `UIWebView/WKWebView or SFSafariViewController` O controlador precisa ser instanciado para poder seguir as operações de redirecionamento HTTP.

O fluxo de logout é diferente do fluxo de autenticação, pois o usuário não precisa interagir com o `UIWebView/WKWebView or SFSafariViewController`  de qualquer maneira. Portanto, o Adobe recomenda que você torne o controle invisível (ou seja, oculto) durante o processo de logout.

É utilizado um padrão semelhante ao fluxo de autenticação. O iOS AccessEnabler aciona o `navigateToUrl:` retorno de chamada ou a variável `navigateToUrl:useSVC:` para criar um `UIWebView/WKWebView or SFSafariViewController` e para carregar o URL fornecido no `url` parâmetro. Esse é o URL do endpoint de logout no servidor de back-end. Para o tvOS AccessEnabler, nenhuma das variáveis `navigateToUrl:` retorno de chamada ou a variável `navigateToUrl:useSVC:` o retorno de chamada é chamado.

Conforme ele passa por vários redirecionamentos, seu aplicativo deve monitorar a atividade do `UIWebView/WKWebView or SFSafariViewController `e detectar o momento em que carrega um URL personalizado específico. Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele só deve ser interpretado pelo seu aplicativo como um sinal de que o fluxo de logout foi concluído e de que é seguro fechar o controlador. Quando o controlador carrega esse URL personalizado específico, seu aplicativo deve fechar o controlador e chamar o `handleExternalURL:url `Método da API. Caso seu aplicativo seja necessário usar um `SFSafariViewController `controladora o URL personalizado específico é definido pelo seu `application's custom scheme` (por exemplo,`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), caso contrário, esse URL personalizado específico será definido pela variável `ADOBEPASS_REDIRECT_URL `constante (ou seja, `adobepass://ios.app`).

No final, o AccessEnabler chamará a função [`setAuthenticationStatus()`](#setAuthNStatus) retorno de chamada com um código de status igual a 0, indicando o sucesso do fluxo de logout.

**Observação:** Se o usuário estiver conectado usando o Apple SSO, o status do VSA203 será acionado. Se esse for o caso, o usuário deve ser instruído a fazer logoff também nas configurações do sistema. Se isso não for feito, haverá uma reautenticação quando o aplicativo for reiniciado.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: iniciar o fluxo de logout</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[Voltar ao topo...](#apis)

</br>

### getSeletedProvider {#getSelProv}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Use este método para determinar o provedor selecionado no momento.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: determinar o MVPD atualmente selecionado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** [`selectedProvider:`](#selProv)

[Voltar ao topo...](#apis)

</br>

### seletedProvider {#selProv}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que fornece informações sobre o MVPD atualmente selecionado para o aplicativo.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: informações sobre o MVPD atualmente selecionado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros**:

* *mvpd*: objeto que contém informações sobre o MVPD atualmente selecionado

**Disparado por:** [`getSelectedProvider`](#getSelProv)

[Voltar ao topo...](#apis)

</br>

### getMetadata: {#getMeta}

**Arquivo:** AccessEnabler/headers/AccessEnabler.h

**Descrição:** Use esse método para recuperar informações expostas como metadados pela biblioteca AccessEnabler . O aplicativo pode acessar esses dados fornecendo um dicionário *key* parâmetro de entrada.

Há dois tipos de metadados disponíveis para Programadores:

* Metadados estáticos (TTL do token de autenticação, TTL do token de autorização e ID do dispositivo) 
* Metadados do usuário (informações específicas do usuário, como ID do usuário, CEP; pode ser transmitido de um MVPD para o dispositivo de um usuário durante os fluxos de Autenticação e Autorização)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chamada da API: consultar os metadados do AccessEnabler</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros:**

* *keyDictionary*: uma estrutura de dados de dicionário, com o seguinte formato:
   * Se a chave for `METADATA_OPCODE_KEY` e o valor é `METADATA_AUTHENTICATION`, o query é feito para obter o tempo de expiração do token de autenticação.
   * Se a chave for `METADATA_OPCODE_KEY` e o valor é `METADATA_AUTHORIZATION` **e**\
      chave é `METADATA_RESOURCE_ID_KEY` e o valor é uma ID de recurso específica, então o query é feito para obter o tempo de expiração do token de autorização associado ao recurso especificado.
   * Se a chave for `METADATA_OPCODE_KEY` e o valor é `METADATA_DEVICE_ID`, então o query é feito para obter a id do dispositivo atual. Observe que esse recurso está desativado por padrão e os programadores devem entrar em contato com o Adobe para obter informações sobre ativação e tarifas.
   * Se a chave for `METADATA_OPCODE_KEY` e o valor é `METADATA_USER_META` **e** chave é `METADATA_USER_META_KEY` e valor é o nome dos metadados, então a consulta é feita para metadados do usuário. A lista de tipos de metadados de usuário disponíveis:
      * `zip` - Lista de códigos postais
      * `householdID` - Identificador da família. Caso um MVPD não suporte subcontas, isso será idêntico ao `userID`.
      * `maxRating` - Uma coleção de classificações máximas dos pais para o usuário
      * `userID` - O identificador do usuário. Se um MVPD suportar subcontas e o usuário não for a conta principal, `userID` será diferente de `householdID.`
      * `channelID` - Uma lista de canais que um usuário tem direito a visualizar.
   >[!NOTE]
   >
   >Os metadados de usuário reais disponíveis para um Programador dependem do que um MVPD disponibiliza. Essa lista será expandida à medida que novos metadados forem disponibilizados e adicionados ao sistema de autenticação do Primetime.

**Retornos de chamada acionados:** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**Mais informações:** [Metadados do usuário](/help/authentication/user-metadata.md)

[Voltar ao topo...](#apis)

</br>

### currentTVProviderDialog {#presentTvDialog}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno acionado pelo AccessEnabler após chamar[getAuthentication()](#getAuthN) se o solicitante atual suportar pelo menos um MVPD com suporte por SSO.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: resultado dos fluxos SSO</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v2.0+

**Parâmetros**:

* viewController: representa a caixa de diálogo SSO do Apple. Esse viewController precisa ser exibido na tela.

**Disparado por:** [`getAuthentication`](#getAuthN)

**Mais informações:** [Logon único do iOS/tvOS](#presentTvDialog)

[Voltar ao topo...](#apis)

</br>

### dismissTVProviderDialog {#dismissTvDialog}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler após o usuário fechar a caixa de diálogo SSO do Apple.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: resultado dos fluxos SSO</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v2.0+

**Parâmetros**:

* viewController: representa a caixa de diálogo SSO do Apple. Esse viewController precisa ser removido da tela.

**Disparado por:** Ação do usuário

**Mais informações:** [Logon único do iOS/tvOS](#presentTvDialog)

[Voltar ao topo...](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que fornece os metadados solicitados por meio de um [`getMetadata:`](#getMeta) chame.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Retorno de chamada: resultado da solicitação de recuperação de metadados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilidade:** v1.0+

**Parâmetros**:

* *metadados*: Os metadados solicitados. Esse valor é uma `NSString` no caso de metadados estáticos (TTL de autenticação, TTL de autorização, ID do dispositivo).  É um objeto complexo ao solicitar metadados específicos do usuário. Esse objeto complexo geralmente é a representação Objetive-C de uma carga JSON (por exemplo, &#39;{&quot;street&quot;: &quot;Avenida Principal&quot;, &quot;edifícios&quot;: [&quot;150&quot;, &quot;320&quot;]}&#39; é traduzido em Objetive-C como NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;building&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;)).   Objeto JSON de metadados de amostra:

```JSON
        {
            updated: 1334243471,
            encrypted: ["encryptedProp"],
            data: {
                zip: ["12345", "34567"],
                maxRating: { 
                    "MPAA": "PG-13",
                    "VCHIP": "TV-Y", 
                    "URL": "http://exam.pl/e/manage/ratings"
                },
                householdID: "3456",
                userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                channelID: ["channel-1", "channel-2"]
            }
```

* *criptografado*: valor booleano que especifica se os metadados recuperados são criptografados ou não. Esse parâmetro é importante somente para solicitações de Metadados do usuário. Ele não tem significado para Metadados estáticos (por exemplo, TTL de autenticação) que são sempre recebidos sem criptografia. Se este parâmetro for definido como true, cabe ao Programador obter o valor de Metadados de Usuário Não criptografados executando uma descriptografia RSA usando a chave privada da lista de permissões (a mesma chave privada usada para a assinatura da ID do Solicitante no [`setRequestor:setSignedRequestorId:`](#setReq) e `setRequestor:setSignedRequestorId:serviceProviders: `chamadas de ).

* *key*: A chave usada para formular a solicitação de recuperação de metadados.

* *argumentos*: O mesmo dicionário passado para [`getMetadata:`](#getMeta) chame. Isso é fornecido para permitir que o aplicativo corresponda as solicitações com as respostas.

**Disparado por:** [`getMetadata:`](#getMeta)

**Mais informações:** [Metadados do usuário](/help/authentication/user-metadata.md)


[Voltar ao topo...](#apis)

</br>

### MVPD {#mvpd}

**Arquivo:** AccessEnabler/headers/model/MVPD.h

**Descrição** Descreve o objeto MVPD. Pode ser usado para obter informações sobre as propriedades do MVPD.

**Disponibilidade:** v1.0+ [A propriedade boardingStatus está disponível na v2.2] 

**Propriedades**:

* (NSString) ID - A ID do MVPD.
* (NSString) displayName - O nome do MVPD. [Isso deve ser usado para exibir no seletor]
* Logotipo (NSString) URL - O endereço do logotipo do MVPD.
* (BOOL) enablePlatformServices - Se for verdadeiro, o MVPD suporta serviços SSO como [Apple SSO](#presentTvDialog).
* (NSString) boardingStatus - Pode ter 3 valores:
   * nil - O MVPD não suporta Apple SSO.
   * PICKER - O MVPD pode aparecer no seletor de Apple, mas o fluxo de autenticação é feito pelo Adobe.
   * SUPORTADO - O MVPD é totalmente compatível com o Apple e usará o token SSO Apple.

[Voltar ao topo...](#apis)

</br>

## Rastreamento de eventos {#tracking}

O AccessEnabler aciona um retorno de chamada adicional que não está necessariamente relacionado aos fluxos de direito. Implementar o [`sendTrackingData()`](#sendTracking) a função de retorno de chamada é opcional, mas permite que o aplicativo rastreie eventos específicos e compile estatísticas, como o número de tentativas de autenticação/autorização bem-sucedidas/com falha. 

### sendTrackingData:forEventType: {#sendTracking}

**Arquivo:** AccessEnabler/headers/EntitlementDelegate.h

**Descrição** Retorno de chamada acionado pelo AccessEnabler que sinaliza para o aplicativo a ocorrência de vários eventos, como a conclusão/falha dos fluxos de autenticação/autorização. Com a autenticação do Primetime 1.6, o tipo de dispositivo, o tipo de cliente AccessEnabler e o sistema operacional são relatados por [`sendTrackingData()`](#sendTracking). O [`sendTrackingData()`](#sendTracking) o retorno de chamada permanece compatível com versões anteriores.

**Retorno de chamada: rastreamento de eventos**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**Disponibilidade:** v1.0+

**Observação:** O tipo de dispositivo e o sistema operacional são derivados por meio do uso de uma biblioteca Java pública (<http://java.net/projects/user-agent-utils>) e a sequência do agente do usuário. Esteja ciente de que essas informações são fornecidas apenas como uma maneira abrangente de detalhar métricas operacionais em categorias de dispositivos, mas o Adobe não pode se responsabilizar por resultados incorretos. Use a nova funcionalidade adequadamente.

* Valores possíveis para o tipo de dispositivo:
   * `computer`
   * `tablet`
   * `mobile`
   * `gameconsole`
   * `unknown`

* Valores possíveis para o tipo de cliente AccessEnabler:
   * `flash`
   * `html5`
   * `ios`
   * `android`


**Parâmetros**:

* *evento*: o código do evento que está sendo rastreado. Há três tipos possíveis de eventos de rastreamento:
   * **authorizationDetection:** sempre que uma solicitação de token de autorização retornar (evento é `TRACKING_AUTHORIZATION`)
   * **authenticationDetection:** sempre que ocorrer uma verificação de autenticação (evento é `TRACKING_AUTHENTICATION`)
   * **mvpdSelection:** quando o usuário seleciona um MVPD no formulário de seleção MVPD (evento é `TRACKING_GET_SELECTED_PROVIDER`)
* *dados*: dados adicionais associados ao evento reportado. Esses dados são apresentados no formato de uma lista de valores.

**Disparado por:** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

Instruções para a interpretação dos valores no *dados* array:

* Para trackingEventType `TRACKING_AUTHENTICATION:`
   * **0** - Se a solicitação de token foi bem-sucedida (true/false) e se foi bem-sucedida:
   * **1** - Cadeia de caracteres de ID de MVPD
   * **2** - GUID (hash md5)
   * **3** - Token já em cache (true/false)
   * **4** - Tipo de dispositivo
   * **5** - Tipo de cliente AccessEnabler
   * **6** - Tipo de sistema operacional

* Para trackingEventType `TRACKING_AUTHORIZATION:`
   * **0** - Se a solicitação de token foi bem-sucedida (true/false) e se foi bem-sucedida:
   * **1** - ID MVPD
   * **2** - GUID (hash md5)
   * **3** - Token já em cache (true/false)
   * **4** - Erro
   * **5** - Detalhes
   * **6** - Tipo de dispositivo
   * **7** - Tipo de cliente AccessEnabler
   * **8** - Tipo de sistema operacional
* Para trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   * **0** - ID do MVPD atualmente selecionado
   * **1** - Tipo de dispositivo
   * **2** - Tipo de cliente AccessEnabler
   * **3** - Tipo de sistema operacional

</br>

## Informações relacionadas {#related}

* [Guia de integração do iOS](/help/authentication/iostvos-sdk-cookbook.md)
* [Visão geral técnica da iOS](/help/authentication/iostvos-sdk-overview.md)
* [Fluxo de direitos](/help/authentication/entitlement-flow.md)
   <!--* [Tracking Data in Primetime authentication](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)-->
