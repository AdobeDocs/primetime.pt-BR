---
title: O fluxo de direito do programador
description: O fluxo de direito do programador
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---


# O fluxo de direito do programador {#prog-entitlement-flow}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Este documento descreve o fluxo de direito básico da perspectiva do Programador.  Para obter informações sobre recursos e casos de uso além da integração TVE básica abordada aqui, consulte [Casos de uso do programador](/help/authentication/programmer-use-cases.md).

A autenticação da Adobe Primetime mede o fluxo de direito entre Programadores e MVPDs fornecendo interfaces seguras e consistentes para ambas as partes.  Do lado do Programador, a autenticação do Primetime fornece dois tipos gerais de interface de direito:

1. AccessEnabler - um componente do cliente que fornece uma biblioteca de APIs para aplicativos em dispositivos que podem renderizar páginas da Web (por exemplo, aplicativos da Web, aplicativos de smartphone/tablet).
2. API sem cliente - Serviços Web RESTful para dispositivos que não podem renderizar páginas da Web (por exemplo, decodificadores, consoles de jogos, TVs inteligentes). O requisito para renderizar páginas da Web vem do requisito do MVPD de que os usuários se autentiquem no site do MVPD.

Além da visão geral neutra em plataforma apresentada aqui, há uma visão geral específica da API sem cliente aqui: Documentação da API sem cliente. O AccessEnabler é executado nativamente em plataformas compatíveis (AS/JS na Web, Objetive-C no iOS e Java no Android). As APIs do AccessEnabler são consistentes em todas as plataformas compatíveis. Todas as plataformas que não oferecem suporte ao AccessEnabler usam a mesma API sem cliente.

Para ambos os tipos de interface, a autenticação do Primetime medeia com segurança o fluxo de direito entre o aplicativo do Programador e o MVPD do usuário:

![](assets/prog-entitlement-flow.png)


*Figura: Ecossistema de autenticação da Adobe Primetime*

>[!IMPORTANT]
>
>Observe no diagrama acima que há uma parte do fluxo de direito que não passa pelos servidores de autenticação da Adobe Primetime: o login do MVPD. Os usuários devem fazer logon na página de logon do MVPD. Devido a esse requisito, em dispositivos que não podem renderizar páginas da Web, o aplicativo do Programador deve direcionar os usuários para um dispositivo com capacidade para a Web para fazer logon com o MVPD, depois eles retornam ao dispositivo original pelo restante do fluxo de direito.

## Fluxo de direitos {#entitlement-flow}

Há quatro sub-fluxos distintos que compõem o fluxo de direito básico:

1. [Fluxo de inicialização](/help/authentication/entitlement-flow.md#startup)
1. [Fluxo de autenticação](/help/authentication/entitlement-flow.md#authentication)
1. [Fluxo de autorização](/help/authentication/entitlement-flow.md#authorization)
1. [Logout do FLow](/help/authentication/entitlement-flow.md#logout)

Na visita inicial de um usuário ao site de um Programador, o fluxo de direito continua na ordem acima. No entanto, em visitas subsequentes, dependendo se os tokens de autenticação e autorização expiraram ou não, ou dependendo das políticas de exibição, um usuário pode passar por um ou dois dos sub-fluxos.

### Fluxo de inicialização {#startup}

Estabelece a identidade do Programador e do dispositivo, executa tarefas de inicialização. Isso é um pré-requisito para todas as chamadas de direito subsequentes.

**AccessEnabler**

* **`setRequestor()`** - Estabelece sua identificação com o AccessEnalber e, por extensão, com os servidores de autenticação da Adobe Primetime. Esta chamada é precursora do resto do fluxo de direito. Por exemplo, em JavaScript:

   ```JavaScript
     /* Define the requestor ID (Programmer/aggregator ID). */
       var requestorID = "sample_requestor_Id";
       ...
       // Callback indicating that the AccessEnabler swf has initialized
       function swfLoaded() {
           // AccessEnabler is loaded so we can use the API function it provides
           accessEnablerObject.setRequestor(requestorID); 
       ...
       }
   ```

**API sem cliente**

* **`\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode`** - Dependendo da plataforma, pode haver tarefas de pré-requisito a serem concluídas antes que o aplicativo chame regcode. Consulte a **Documentação da API sem cliente** para obter detalhes. Por exemplo, as plataformas Xbox exigem que você complete as etapas de segurança prescritas antes de chamar o regcode.

### Fluxo de autenticação {#authentication}

Autenticação bem-sucedida gera um token AuthN vinculado ao dispositivo e ao solicitante. A autenticação bem-sucedida é um pré-requisito para a Autorização.

**AccessEnabler**

* `checkAuthentication()` - Verifica se existe um token de autenticação em cache válido no cache de token local, sem realmente acionar o fluxo de autenticação completo. Isso aciona o `setAuthenticationStatus()` função de retorno de chamada.
* `getAuthentication()` - Inicia o fluxo de autenticação completo. Se bem-sucedido, a autenticação da Adobe Primetime gera um token AuthN e o armazena em cache no cliente. O usuário faz logon no site MVPDs selecionado, apresentado em um iFrame, uma janela Pop-up ou uma visualização da Web, dependendo da plataforma. Isso aciona displayProviderDialog().

**API sem cliente**

* `<FQDN>/.../checkauthn` - A versão do serviço da Web de `checkAuthentication()` acima.
* `<FQDN>/.../config` - Retorna a lista de MVPDs para o aplicativo de segunda tela.
* `<FQDN>/.../authenticate` - Inicia o fluxo de autenticação a partir do aplicativo de segunda tela, redirecionando os usuários para o MVPD selecionado para logon. Se bem-sucedido, a autenticação do Adobe Primetime gera um token AuthN e o armazena no servidor, e o usuário retorna ao dispositivo original para concluir o fluxo de direito.

Um token AuthN é considerado válido se os dois pontos a seguir forem verdadeiros:

* O token AuthN não expirou
* O MVPD associado ao token AuthN está na lista de MVPDs permitidos para a ID do Solicitante atual

#### Fluxo de trabalho de autenticação inicial do AccessEnabler genérico {#generic-ae-initial-authn-flow}

1. Seu aplicativo inicia o fluxo de trabalho de autenticação com uma chamada para `getAuthentication()`, que verifica se há um token de autenticação em cache válido. Este método tem um `redirectURL` parâmetro; se você não fornecer um valor para `redirectURL`, após uma autenticação bem-sucedida, o usuário é retornado ao URL do qual a autenticação foi inicializada.
1. O AccessEnabler determina o status de autenticação atual. Se o usuário estiver autenticado no momento, o AccessEnabler chamará seu `setAuthenticationStatus()` função de retorno de chamada, transmitindo um status de autenticação indicando sucesso.
1. Se o usuário não estiver autenticado, o AccessEnabler continuará o fluxo de autenticação determinando se a última tentativa de autenticação do usuário foi bem-sucedida com um determinado MVPD. Se uma ID MVPD estiver armazenada em cache E a variável `canAuthenticate` sinalizador é verdadeiro OU um MVPD foi selecionado usando `setSelectedProvider()`, o usuário não é solicitado com a caixa de diálogo de seleção MVPD. O fluxo de autenticação continua usando o valor em cache do MVPD (ou seja, o mesmo MVPD que foi usado durante a última autenticação bem-sucedida). Uma chamada de rede é feita no servidor de back-end e o usuário é redirecionado para a página de logon do MVPD.

1. Se nenhuma ID MVPD estiver armazenada em cache E nenhum MVPD tiver sido selecionado usando `setSelectedProvider()` OU a `canAuthenticate` sinalizador é definido como falso, a variável `displayProviderDialog()` o retorno de chamada é chamado. Este retorno de chamada direciona seu aplicativo para criar a interface do usuário que apresenta a ele uma lista de MVPDs para escolher. Uma matriz de objetos MVPD é fornecida, contendo as informações necessárias para você criar o seletor MVPD. Cada objeto MVPD descreve uma entidade MVPD e contém informações como a ID do MVPD e a URL onde o logotipo MVPD pode ser encontrado.

1. Depois que um MVPD é selecionado, seu aplicativo deve informar o AccessEnabler da escolha do usuário. Para clientes que não são Flash, depois que o usuário seleciona o MVPD desejado, você informa o AccessEnabler da seleção do usuário por meio de uma chamada para o `setSelectedProvider()` método . Os clientes do Flash, em vez disso, despacham um `MVPDEvent` do tipo &quot;`mvpdSelection`&quot;, transmitindo o provedor selecionado.

1. Quando o AccessEnabler é informado sobre a seleção de MVPD do usuário, uma chamada de rede é feita ao servidor de back-end e o usuário é redirecionado para a página de logon do MVPD.

1. No workflow de autenticação, o AccessEnabler se comunica com a autenticação Adobe Primetime e o MVPD selecionado para solicitar as credenciais do usuário (ID de usuário e senha) e verificar sua identidade. Embora alguns MVPDs sejam redirecionados para seu próprio site para o logon, outros exigem que você exiba sua página de logon em um iFrame. Sua página deve incluir o retorno de chamada que cria um iFrame, caso o cliente escolha um desses MVPDs.<!-- For more information on creating a login iFrame, see  [Managing the Login IFrame](https://tve.helpdocsonline.com/managing-the-login-iframe)-->.

1. Depois que o usuário faz logon com êxito, o AccessEnabler recupera o token de autenticação e informa ao aplicativo que o fluxo de autenticação foi concluído. O AccessEnabler chama a função `setAuthenticationStatus()` retorno de chamada com um código de status 1, indicando sucesso. Se houver um erro durante a execução dessas etapas, a variável `setAuthenticationStatus()` O retorno de chamada é acionado com um código de status de 0, indicando falha de autenticação, bem como um código de erro correspondente.

>[!IMPORTANT]
>O Comcast é o único MVPD no momento que não fornece um URL estático para o logotipo. Os programadores devem obter os logotipos mais recentes atualizados de [Portal do desenvolvedor XFINITY](https://developers.xfinity.com/products/tv-everywhere).

### Fluxo de autorização {#authorization}

A autorização é um pré-requisito para visualizar conteúdo protegido. A autorização bem-sucedida gera um token AuthZ, juntamente com um token de mídia de curta duração fornecido ao aplicativo do Programador para fins de segurança. Observe que, para ser compatível com o fluxo de trabalho de autorização, você deve ter executado previamente a configuração necessária do solicitante e integrado o [Verificador de token de mídia](/help/authentication/media-token-verifier-int.md). Com essas alterações concluídas, você poderá iniciar a autorização.

Seu aplicativo inicia a autorização quando um usuário solicita acesso a um recurso protegido. Você passa uma ID de recurso especificando o recurso solicitado (por exemplo, um canal, um episódio, etc.). Seu aplicativo verifica primeiro se há um token de autenticação armazenado. Se uma não for encontrada, você iniciará o processo de autenticação.

**AccessEnabler**

* `checkAuthorization()` - Verifica a autorização sem iniciar o fluxo de autorização total. Geralmente, isso é usado para atualizar as informações de status exibidas na interface do usuário do aplicativo do Programador.

* `getAuthorization()` - Inicia o fluxo de autorização completo.

Você fornece as seguintes funções de retorno de chamada para lidar com os resultados da chamada de autorização:

* `setToken()` - Se a autenticação tiver sido bem-sucedida anteriormente e a autorização for bem-sucedida, o AccessEnabler chamará seu `setToken()` função de retorno de chamada, transmitindo o token de mídia de duração curta, indicando uma conclusão bem-sucedida ao fluxo de direito de autenticação do Adobe Primetime. (Antes de permitir que o usuário visualize conteúdo protegido, o aplicativo do Programador verifica a validade do token de mídia usando o Verificador de token de mídia.

* `tokenRequestFailed()` - Se o usuário não estiver autorizado para o recurso solicitado (ou se a consulta falhar por qualquer outro motivo), o AccessEnabler chama essa função de retorno de chamada (além de suas próprias funções de relatório de erros), transmitindo detalhes sobre a falha.

**API sem cliente**

* `\<FQDN\>/.../authorize` - Inicia o fluxo de autorização completo.

#### Fluxo de trabalho de autorização genérico do AccessEnabler {#generic-ae-authr-wf}

1. Forneça uma função de retorno de chamada que registre o GUID do programador atribuído com o Ativador de acesso, usando `setReqestor()`. Essa função de retorno de chamada é chamada quando o AccessEnabler é baixado com êxito.

1. Chame `getAuthorization()` quando um usuário solicita acesso a um recurso protegido. Usando `getAuthorization()`, passe uma ID de recurso especificando o recurso solicitado (por exemplo, um canal, episódio, etc.). O AccessEnabler procura que um token de autenticação em cache passe com a solicitação de autorização. Se uma não for encontrada, ela iniciará o fluxo de autenticação.
1. Forneça funções de retorno de chamada para lidar com os resultados da autorização:

   * `setToken()` - Se a autorização tiver êxito ou se o usuário tiver sido autorizado anteriormente, o Ativador de Acesso continuará com o processo de autorização, chamando seu `setToken()` função de retorno de chamada, transmitindo o token de autorização de duração curta.

   * `tokenRequestFailed()` - Se o usuário não estiver autorizado para o recurso solicitado (ou se a consulta falhar por qualquer outro motivo), o AccessEnabler chamará quaisquer funções de relatório de erros que você tenha registrado, além do `tokenRequestFailed()` retorno de chamada, transmitindo detalhes sobre a falha.

### Fluxo de logout {#logout}

Apaga tokens e outros dados associados ao fluxo de direito do usuário atual.

**AccessEnabler**

* `logout()`

**API sem cliente**

* `\<FQDN\>/.../logout`

## Compreender o comportamento do AccessEnabler {#ae-behavior}

Todas as chamadas da API do AccessEnabler são assíncronas (com uma exceção, anotada nas referências da API). Você pode chamar uma API um número arbitrário de vezes, no entanto, não há garantia forte de que as ações acionadas pelas chamadas sejam concluídas na mesma ordem em que as chamadas foram feitas. (Uma exceção a isso é o tempo de execução atual do Flash Player; não sendo multi-segmentado, ele garantirá chamadas *do* complete na ordem em que são chamados.)

Para distinguir entre respostas e poder emparelhar respostas com chamadas, todos os retornos de chamada repetem seus parâmetros de entrada. Isso inclui `setToken()` e`tokenRequestFailed()`, que, em última análise, são acionados por `checkAuthorization()`. (Para `checkAuthorization()` retornos de chamada, o recurso usado é repetido.) Aproveitando esse recurso, você pode distinguir qual resposta corresponde a qual chamada. Para usar esse recurso, você pode codificar algo como o seguinte:

```JavaScript
    for each (resource in ["TNT", "CNN", "TBS", "AdultSwim"] ) {
         ae.checkAuthorization(resource);
    }
    
    // Success callback
    function setToken(resource, token) {
         // Use "resource" to figure 
         // out which checkAuthorization
         // call triggered this response
    }
    
    // Old error callback
    function tokenRequestFailed(resource, error, details) {
         // use "resource" to figure
         // out in response to which
         // checkAuthorization call
         // this was triggered
    }
    
    // Error callback using new error api
    ae.bind("errorEvent',"errorHandler");
    
    function errorHandler(error) {
         if(error.resource) {        
              // Use error.resource to figure
              // which checkAuthorization call
              // triggered this response
         }
    }
```

### Perguntas frequentes sobre o comportamento no AEM {#ae-beh-faq}

**Pergunta. O que acontece se eu fizer uma segunda chamada AccessEnabler antes da conclusão da primeira chamada?**

A primeira chamada continua sendo executada conforme a segunda chamada é executada (comunicações assíncronas).

**Pergunta. Existe um número máximo de chamadas simultâneas que o AccessEnabler pode suportar?**

Nenhum limite é definido explicitamente no código AccessEnabler, de modo que você é limitado somente pelos recursos disponíveis do sistema, bem como pela capacidade do MVPD.

<!--

>[!MORELIKETHIS]
>
>*   [Programmer use cases](/help/authentication/programmer-use-cases.md)
>*   Error Reporting
>**Platform Cookbooks:**
>*   Clientless integration cookbook
>*   iOS Integration Cookbook
>*   Android Integration Cookbook
>*   JavaScript Integration Cookbook
>*   ActionScript Integration Cookbook
>*   Windows 8 Integration Cookbook
>*   AIR Native Extension Overview
-->