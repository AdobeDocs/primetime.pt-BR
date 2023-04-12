---
title: Escopo do Provedor de Serviços
description: Escopo do Provedor de Serviços
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Escopo do Provedor de Serviços {#service-provoider-scoping}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

A implementação padrão de uma integração de autenticação da Adobe Primetime com um MVPD é baseada no **Especificação OLCA**. A seção Requisitos de Autenticação da especificação OLCA (6.5, Identificador do Assunto) afirma que é possível indicar o escopo do Provedor de Serviços (SP) para o identificador do Assunto. (O identificador de assunto é a ID de usuário ofuscada que o MVPD retorna ao SP.)  Em uma integração de autenticação da Adobe Primetime, é necessário que os MVPDs habilitem o escopo das solicitações de Autenticação da SP.

Com a autenticação da Adobe Primetime assumindo a função de SP para o Programador, é necessário implementar uma personalização que permita o escopo de SP da solicitação de Autenticação.  Isso precisa ser feito para que o MVPD possa identificar a marca de rede transmitida na asserção SAML ao Provedor de Identidade (IdP) do MVPD.  O escopo pode ser implementado de uma das duas maneiras descritas na próxima seção.

## Escopo do Provedor de Serviços {#service-provider-scoping}

A autenticação do Adobe Primetime oferece suporte às duas formas a seguir para habilitar o escopo SP de solicitações de Autenticação:

* **Abordagem do emissor SAML.**  Nessa abordagem, a &quot;ID do solicitante&quot; é anexada à string do emissor do SAML na solicitação de autenticação do SAML.

* **A Abordagem De Propriedade De Escopo Personalizada.**  Nesta abordagem, a &quot;ID do solicitante&quot; é incluída explicitamente como uma propriedade personalizada &quot;Escopo&quot; na solicitação de autenticação SAML.

>[!NOTE]
>
>A &quot;ID do solicitante&quot; é como a autenticação da Adobe Primetime se refere à marca de rede do programador (por exemplo: &quot;CNN&quot; é uma das marcas da rede Turner).

### Abordagem do Emissor SAML {#saml-issuer-approach}

Essa abordagem usa o SAML `<Issuer>` na solicitação de autenticação SAML, como mostrado neste trecho:

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### Abordagem de propriedade de escopo personalizado {#custom-scoping-property-approach}

Essa abordagem usa uma propriedade personalizada chamada &quot;Escopo&quot;, conforme mostrado neste trecho de uma solicitação de autenticação SAML:

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->