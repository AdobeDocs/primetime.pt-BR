---
title: Troca de metadados de conteúdo MVPD
description: Troca de metadados de conteúdo MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Troca de metadados de conteúdo MVPD

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#content-metadat-exchange-overview}

Esta página descreve duas implementações padrão que a autenticação da Adobe Primetime usa para enviar dados estruturados para MVPDs na solicitação de Autorização.  Os dados estruturados representam o recurso (o Programador) que faz a solicitação e, possivelmente, dados adicionais, como a classificação de conteúdo.

No lado do Programador, a autenticação do Adobe Primetime suporta recursos de dados MRSS estruturados da seguinte maneira:

1. O Programador envia o Recurso como uma string MRSS. A autenticação da Adobe Primetime não a codifica no lado do cliente para dispositivos da Web ou nativos. O MRSS é enviado como uma string regular para o servidor de autenticação da Adobe Primetime.
1. No lado do servidor, o MRSS é validado em relação ao esquema predefinido (http://search.yahoo.com/mrss/).  Se a validação for aprovada, a autenticação do Adobe Primetime extrairá as informações dos campos MRSS, incluindo:
   * título do canal
   * título do item
   * identificador de recurso
   * valor e tipo de classificação
1. Os valores extraídos do MRSS são utilizados para criar o pedido de autorização passado para o MVPD.

A autenticação Adobe Primetime suporta duas abordagens para converter o MRSS em formatos suportados por MVPDs:

* **XACML**.  A primeira abordagem se alinha ao padrão OLCA.  Ele usa o XACML, no qual os valores de MRSS são extraídos para criar um XACMLResource com atributos que mapeiam para os elementos de MRSS.  Isso é então passado para o MVPD.
* **REST**.  A segunda abordagem é baseada em REST.  O MRSS é codificado em base64 e passado como um parâmetro de URL na chamada REST.

Em ambas as abordagens, o MVPD processa o pedido de autorização incluindo os valores extraídos dentro do seu próprio fluxo lógico e devolvendo uma resposta de autorização.

## Detalhes da integração {#integration-details}

* Recurso Estruturado XACML baseado em OLCA
* Recurso Estruturado baseado em REST

### Recurso Estruturado XACML baseado em OLCA {#olca-based-xacml-struc-resource}

A maioria dos MVPDs orientados a cabo usam a abordagem baseada em XACML, mas ainda não oferecem suporte à abordagem de dados totalmente estruturados.  Outros MVPDs que suportam XACML tomam o Título do Canal e aceitam isso para o atributo ResourceID. O exemplo abaixo mostra a abordagem totalmente estruturada baseada em XACML. A equipe de autenticação da Adobe Primetime recomenda que, para MVPDs que usam XACML, mas ainda não oferecem suporte a recursos como controles dos pais, eles adaptem sua integração XACML ao seguinte exemplo:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability
```

### Recurso Estruturado baseado em REST {#rest-based-struct-resource}

Alguns MVPDs padronizaram o seguinte protocolo baseado em REST para autorização. Essa abordagem é tão completa quanto a abordagem XACML, mas fornece uma implementação de &quot;peso mais leve&quot;.

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->