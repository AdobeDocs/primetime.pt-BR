---
title: Escopo do provedor de serviços
description: Escopo do provedor de serviços
exl-id: 730c43e1-46c0-4eec-b562-b1ad93cce6d3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Escopo do provedor de serviços {#service-provoider-scoping}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Visão geral {#overview}

A implementação padrão de uma integração de autenticação do Adobe Primetime com um MVPD é baseada no **Especificação OLCA**. A seção Authentication Requirements da especificação OLCA (6.5, Subject Identifier) indica que é possível indicar o escopo do Service Provider (SP) para o identificador de assunto. (O identificador de assunto é a ID de usuário ofuscada que o MVPD retorna à controladora.)  Em uma integração de autenticação do Adobe Primetime, é necessário que os MVPDs habilitem o escopo das solicitações de autenticação do SP.

Com a autenticação do Adobe Primetime assumindo a função de SP para o Programador, é necessário implementar uma personalização que permita o escopo de SP da solicitação de autenticação.  Isso precisa ser feito para que o MVPD possa identificar a marca de rede transmitida na asserção SAML para o Provedor de identidade (IdP) do MVPD.  O escopo pode ser implementado de uma das duas maneiras descritas na próxima seção.

## Escopo do provedor de serviços {#service-provider-scoping}

A autenticação do Adobe Primetime oferece suporte às duas formas a seguir para habilitar o escopo das solicitações de autenticação da controladora de armazenamento:

* **A Abordagem de Emissor SAML.**  Nesta abordagem, a &quot;ID do solicitante&quot; é anexada à string do emissor SAML na solicitação de autenticação SAML.

* **A Abordagem De Propriedade Do Escopo Personalizado.**  Nesta abordagem, a &quot;ID do solicitante&quot; é incluída explicitamente como uma propriedade personalizada &quot;Escopo&quot; na solicitação de autenticação SAML.

>[!NOTE]
>
>A &quot;ID do solicitante&quot; é como a autenticação da Adobe Primetime se refere à marca de rede do programador (por exemplo: &quot;CNN&quot; é uma das marcas da rede Turner).

### Abordagem de emissor SAML {#saml-issuer-approach}

Essa abordagem usa o SAML `<Issuer>` elemento na solicitação de Autenticação SAML, conforme mostrado neste trecho:

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### Abordagem de propriedade de escopo personalizado {#custom-scoping-property-approach}

Essa abordagem usa uma propriedade personalizada chamada &quot;Escopo&quot;, como mostrado neste trecho de uma solicitação de autenticação SAML:

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
