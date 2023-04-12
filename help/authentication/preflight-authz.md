---
title: Autorização de comprovação
description: Autorização de comprovação
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---



# Autorização de comprovação {#preflight-authorization}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Visão geral {#overview}

Este recurso fornece uma verificação de autorização leve para vários recursos. A finalidade dessa verificação leve é decorar a interface do usuário (por exemplo, indicando o status de acesso com ícones de bloqueio e desbloqueio). A autorização de comprovação é tão leve e eficiente quanto possível, de modo que uma única chamada de API produz o status de autorização para uma lista de recursos. Observe que esse recurso não é autoritativo em relação à autorização de um recurso.

A `getAuthorization(resource)` ou `checkAuthorization(resource)` A chamada ainda DEVE ser feita antes de permitir a reprodução.

A autorização de comprovação também fornece suporte para um caso de uso diferente, em que o Programador precisa solicitar autorização para várias IDs de recurso para permitir a reprodução de um item de conteúdo de mídia. O Programador pode fazer uma verificação de comprovação inicial dos recursos necessários e, dependendo da resposta, pode falhar cedo se as condições comerciais não forem atendidas.

Para obter uma lista de MVPDs que oferecem suporte à autorização de comprovação, consulte o [Autorização de Comprovação de MVPD](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) página. 

>[!NOTE]
>
> Observe que a utilização deste recurso para os MVPDs que não têm suporte total de autorização de comprovação precisa ser acordada antecipadamente com o Adobe &amp; MVPDs. A utilização da autorização de voo prévio nestes MVPDs será incluída no &quot;pior cenário&quot; descrito [here](/help/authentication/mvpd-preflight-authz.md#intro) e pode levar a problemas de desempenho e tempo de resposta lento. </br>
> Além disso, note que a utilização da autorização de comprovação com **mais de 5 recursos precisam ser explicitamente aprovados pelo Adobe**.

## API de comprovação do AccessEnabler {#AE_pre_api}

O AccessEnabler expõe um par de funções de chamada/API para implementar a autorização de comprovação. A chamada da API utiliza um único parâmetro que consiste em uma lista de recursos. A função de retorno de chamada recebe um único parâmetro que representa os recursos autorizados reais. Os exemplos a seguir estão no ActionScript, mas as chamadas estão disponíveis em todas as opções do AccessEnabler.

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

Chame essa função no objeto AccessEnabler para solicitar o status de autorização para uma lista de recursos.

O parâmetro resources é a lista de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID do recurso está sujeita às mesmas limitações que a ID do recurso na `getAuthorization()` ou seja, é acordado o valor estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia. Observe que a autenticação do Adobe Primetime não gerencia recursos de nenhuma maneira, exceto por uma camada de mediação fina que pode transformar formatos de recursos dependendo do que o MVPD realmente suporta.

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

Esta é uma função de retorno de chamada que deve ser implementada no aplicativo de camada superior do Programador. O AccessEnabler chamará essa função após calcular a lista de recursos autorizados.


### Exemplo de JS

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## Informações de implementação {#details}

- [Comprovação usando ChannelID](#preflight_using_channelID)
- [POST / Pré-autorizar](#post)
- [Armazenamento](#storage)

A chamada da API tenta encontrar uma lista em cache de recursos autorizados para o usuário atual no armazenamento local do cliente. Se não houver uma lista em cache, uma chamada HTTPS será feita aos servidores do AdobePass para recuperar a lista.

O mecanismo de armazenamento em cache melhora os tempos de desempenho em chamadas subsequentes ignorando completamente a chamada de rede. Além disso, a lista em cache pode ser preenchida antecipadamente como parte do processo de autenticação.  (Para obter informações sobre como configurar esse cenário, consulte [Integração de autorização de comprovação](/help/authentication/authz-usecase.md#preflight_authz_int) na seção Autorização do Guia de Integração do MVPD).

Além disso, a lista de recursos em cache pode ser potencialmente usada para otimizar o fluxo de autorização, no sentido de que, se existir uma lista de recursos em cache, `checkAuthorization()` pode verificá-lo antes de fazer uma chamada de rede. Se o recurso não estiver na lista de recursos pré-autorizados, a verificação poderá falhar sem precisar chamar os servidores de autenticação do Primetime.


### Comprovação usando ChannelID {#preflight_using_channelID}

A partir da versão 2.4.1 da autenticação do Primetime, o fluxo de Comprovação funciona da seguinte maneira:

1. Durante a autenticação, a autenticação do Primetime lê a variável `channelIID` elemento da resposta SAML do MVPD e usa esse valor para definir a variável `authorizedResources` no token de autenticação.
1. Dentro do `checkPreauthorizedResources()` função da API, a autenticação do Primetime verifica se a variável `authorizedResources` está definido.
1. Se a variável `authorizedResources` estiver definido, a autenticação do Primetime lê esse valor e executa uma interseção entre a lista de recursos da `authorizedResources` e a lista de recursos recebidos de `checkPreauthorizedResources()` parâmetro.  O resultado dessa interseção é a lista final de recursos pré-autorizados.
1. Se a variável `authorizedResources` não estiver definido, execute o fluxo implementado anteriormente, no qual a lista de recursos recebidos de `checkPreauthorizedResources()` é passado para PreAuthorizationServlet. Este servlet executa as chamadas de autorização para os endpoints do MVPD e retorna a lista de recursos pré-autorizados.

### Exemplo de comprovação com ChannelID

O exemplo abaixo mostra uma lista de canais de amostra. Observe que o nome do atributo usado para enviar a lista de canais pode ser diferente de um MVPD para outro:

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

O `authorizedResources` O elemento do elemento de autenticação é exibido da seguinte maneira:

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

O programador executa o `checkPreauthorizedResources()` Chamada de API, transmitindo a seguinte lista de parâmetros:</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

A implementação de comprovação atual executa a interseção com a lista de recursos do `authorizedResources` e retorna esta lista:

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**Observação:** Observe que a interseção não diferencia maiúsculas de minúsculas.

 

### POST / Pré-autorizar {#post}

Essa chamada será executada automaticamente pelo AccessEnabler quando não existir uma lista de recursos em cache, autorizada. 


#### Solicitação {#req}

| Parâmetro | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `authentication_token` | string | SIM | O token de autenticação. |
| `resource_id` | string | SIM | Um único recurso. Isso pode ser especificado várias vezes, uma vez para cada elemento da matriz de recursos fornecida no `checkPreauthorizedResources()` Chamada de API. |


**Observação:** O número máximo de recursos solicitados é configurável.
**O valor padrão máximo é 5.**


#### Resposta {#resp}

A resposta que o servlet pré-autorizado envia de volta tem o seguinte formato:

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### Armazenamento {#storage}

Uma lista de recursos pré-autorizados que o AccessEnabler obtém do Provedor de Serviços. Esta lista de recursos:

- É armazenado juntamente com os tokens AuthN e AuthZ
- É válido desde que o usuário esteja no mesmo site ou até que o token AuthN expire
- É recuperado sempre que o usuário chega a um novo site integrado de autenticação do Primetime

Cada entrada contém a ID de recurso para a qual o usuário está pré-autorizado.

Por exemplo:


| ID do recurso | Autorizado |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


Essa lista é chamada de &quot;cache de pré-autorização&quot;.

#### Fluxo {#flow}

1. O aplicativo/site do programador cria um `checkPreauthorizedResources(resourceList)` chame.
1. O AccessEnabler verifica o token de autenticação para recursos autorizados:
   1. Se o token de autenticação contiver recursos autorizados, essa lista será autoritativa e nenhuma chamada deverá ser feita para obter essas informações. Os recursos do resourceList são pesquisados na lista de recursos autorizados no token de autenticação e somente aqueles que foram encontrados são retornados pela variável `preauthorizedResources()` retorno de chamada.
   1. Se o token de autenticação NÃO contiver recursos autorizados - `resourceList` é comparado à lista de recursos no cache de pré-autorização.
      1. Se a lista contiver os mesmos recursos - isso significa que uma chamada para o servidor já foi feita e a resposta já está no cache de pré-autorização. Somente os recursos autorizados serão retornados pela variável `preauthorizedResources()` retorno de chamada.
      1. Se a lista NÃO contiver os mesmos recursos - o cliente precisará fazer uma chamada para o servidor para obter o estado de autorização para os recursos em resourceList. A resposta será obtida e armazenada no cache de pré-autorização, substituindo completamente os recursos antigos. Somente os recursos autorizados serão retornados pela variável `preauthorizedResources()` retorno de chamada.


#### Recuperação de lista {#listRetrieve}

Sempre que uma `checkPreauthorizedResources()` for chamado, a lista de recursos a serem verificados para autorização será verificada em relação ao cache de pré-autorização. Se a lista contiver o mesmo conjunto de recursos, nenhuma chamada para o Provedor de serviços será feita, pois todos os recursos necessários para acionar a variável `preauthorizedResources()` O retorno de chamada já está no cache.


#### logout() {#logout}

O cache de pré-autorização é esvaziado durante o logout.


## Dependências {#depends}

O desempenho da API de comprovação depende de implementações específicas de MVPD.  Para obter as opções de implementação, consulte [Integração de autorização de comprovação](/help/authentication/authz-usecase.md#preflight_authz_int) na seção Autorização do Guia de Integração do MVPD.


## Segurança {#security}

As APIs do cliente estão disponíveis para todos os programadores.

A implementação usa HTTPS como um transporte, mas para ter uma chamada mais leve, nenhuma medida de segurança adicional é empregada (sem assinatura, sem FAXS).

**Atenção:** NÃO use essa API de uma maneira autoritativa para determinar se um usuário deve receber acesso a um recurso protegido. A finalidade dessa API é a decoração da interface do usuário e/ou a comprovação de decisões comerciais. O `getAuthorization()` e `checkAuthorization()` As chamadas devem sempre ser feitas antes de permitir a reprodução.


## Compatibilidade {#compat}

Este recurso é compatível com todas as opções do AccessEnabler: AS, JS, AIR, iOS, Android, Xbox (em fluxo de AuthN de segunda tela).

A autorização de comprovação não oferece suporte a recursos de pré-autorização que contêm seções CDATA. O foco do sistema de comprovação atual é suportar a filtragem no nível do canal. Os recursos com seções CDATA são provavelmente recursos no nível do ativo. A comprovação oferece suporte simples `mrss` recursos para pré-autorização no nível do canal, desde que não contenham CDATA. 

## Integração com outros recursos {#integ_w_other_features}

Uma possível otimização pode ocorrer no fluxo de autorização para falhar rapidamente se o recurso não estiver na lista de recursos pré-autorizados.

Nessa otimização, o endpoint de comprovação do servidor é integrado ao mecanismo de degradação.  

Se uma regra &quot;AuthN All&quot; estiver em vigor para o MVPD e o Requestor, o terminal de comprovação simplesmente refletirá todos os recursos recebidos na solicitação.

O mesmo é verdadeiro se &quot;AuthZ All&quot; estiver ativado para pelo menos um dos recursos presentes na solicitação.

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
