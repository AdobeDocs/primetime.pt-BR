---
title: Autorização de Comprovação de MVPD
description: Autorização de Comprovação de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---


# Autorização de Comprovação de MVPD

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#mvpd-preflight-authz-intro}

&quot;Autorização de comprovação&quot; é uma verificação de autorização leve para vários recursos. Os programadores o usam principalmente para decorar suas interfaces de usuário (por exemplo, indicando o status de acesso com ícones de bloqueio e desbloqueio).

No momento, a autenticação do Adobe Primetime pode oferecer suporte à Autorização de comprovação de duas maneiras para MVPDs, seja por meio de atributos de resposta AuthN ou por meio de uma solicitação multicanal AuthZ.  Os seguintes cenários descrevem o custo/benefício das diferentes maneiras de implementar a autorização de comprovação:

* **Cenário de Melhor Caso** - O MVPD fornece a lista de recursos pré-autorizados durante a fase de autorização (Multi-channel AuthZ).
* **Cenário de pior cenário** - Se um MVPD não oferecer suporte a nenhuma forma de autorização de vários recursos, o servidor de autenticação da Adobe Primetime executará uma chamada de autorização para o MVPD para cada recurso na lista de recursos. Este cenário tem um impacto (proporcional ao número de recursos) no tempo de resposta da solicitação de autorização de comprovação. Ele pode aumentar a carga nos servidores Adobe e MVPD, causando problemas de desempenho. Além disso, ele gerará eventos de solicitações / respostas de autorização sem a necessidade real de uma reprodução.
* **Obsoleto** - O MVPD fornece a lista de recursos pré-autorizados durante a fase de autenticação, de modo que não haverá chamadas de rede necessárias, nem mesmo a solicitação de comprovação, já que a lista é armazenada em cache no cliente.

Embora os MVPDs não tenham de suportar a autorização de comprovação, as seções a seguir descrevem alguns métodos de autorização de comprovação que a autenticação da Adobe Primetime pode suportar, antes de voltar ao pior cenário de caso acima.

## Comprovação no AuthN {#preflight-authn}

Este cenário de comprovação é Compatível com OLCA (Cableabs). A seção 7.5.2 da Especificação da Interface de Autenticação e Autorização 1.0, intitulada &quot;Instrução de Atributo Dentro da Asserção de Autenticação&quot;, descreve como uma resposta de autenticação SAML pode conter uma lista de recursos pré-autorizados. Se um IdP suportar isso, o servidor de autenticação da Adobe Primetime poderá gerar a lista de recursos predefinidos no momento da autenticação e armazená-la em cache no cliente junto com o Token de autenticação. Esse método também obtém o melhor cenário de caso, e nenhuma chamada de rede será executada quando o Programador chamar checkPreauthorizedResources(), pois tudo já está no cliente.

### Lista de recursos personalizados na instrução de atributos SAML {#custom-res-saml-attr}

A resposta de autenticação SAML do IdP deve incluir uma AttributeStatement contendo nomes de recursos que o AdobePass deve autorizar.  Alguns MVPDs fornecem isso no seguinte formato:

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

A amostra acima apresenta uma lista contendo dois recursos pré-autorizados: &quot;MMOD&quot; e &quot;Olimpíadas 2012&quot;.

Isso efetivamente atinge o melhor cenário de caso, e nenhuma chamada de rede será executada quando o Programador chamar checkPreauthorizedResources(), já que tudo já está no cliente.

## Comprovação de vários canais no AuthZ {#preflight-multich-authz}

Essa implementação de comprovação também é compatível com OLCA (Cablelabs).  A Especificação da Interface de Autenticação e Autorização 1.0 (seções 7.5.3 e 7.5.4) descreve métodos para solicitar informações de Autorização de um MVPD usando Asserções SAML ou XACML. Essa é a maneira recomendada de consultar o status de autorização para MVPDs que não oferecem suporte a isso como parte do fluxo de autenticação. A autenticação da Adobe Primetime emite uma única chamada de rede para o MVPD para recuperar a lista de recursos autorizados.


A autenticação da Adobe Primetime recebe a lista de recursos do aplicativo do Programador. A integração MVPD da autenticação da Adobe Primetime pode fazer uma chamada AuthZ incluindo todos esses recursos e, em seguida, analisar a resposta e extrair as várias decisões de permissão/negação.  O fluxo para a comprovação com o cenário AuthZ de vários canais funciona da seguinte maneira:

1. O aplicativo do Programador envia uma lista separada por vírgulas de recursos por meio da API do cliente de comprovação, por exemplo: &quot;TestChannel1,TestChannel2,TestChannel3&quot;.
1. A chamada de solicitação de pré-voo AuthZ do MVPD contém os vários recursos e tem a seguinte estrutura:

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## Autorização Personalizada Para Vários Recursos {#custom-authz}

Alguns MVPDs têm endpoints de autorização que oferecem suporte à autorização para vários recursos em uma solicitação, mas não se enquadram no cenário descrito em Multi-channel AuthZ. Esses MVPDs específicos exigem trabalho personalizado.

O Adobe também pode suportar autorização de vários canais sem alterações na implementação existente.  Essa abordagem precisa ser revista entre o Adobe e a equipe técnica do MVPD para garantir que funcione conforme esperado.

## MVPDs que oferecem suporte à autorização de comprovação {#mvpds-supp-preflight-authz}

A tabela a seguir lista os MVPDs que oferecem suporte à Autorização de Comprovação, juntamente com o tipo de comprovação que eles suportam e as limitações conhecidas:

| Abordagem de comprovação | MVPD | Notas |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| AuthZ multicanal | Comcast Proxy AT&amp;T Clearleap Letter_Direct Proxy GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |  |
| Lineup de canal em metadados do usuário | Suddenlink HTC | Todas as integrações diretas do Synacor também podem suportar essa abordagem. |
| Bifurcar e unir | Todos os outros não listados acima | O número máximo padrão de recursos marcados = 5. |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->