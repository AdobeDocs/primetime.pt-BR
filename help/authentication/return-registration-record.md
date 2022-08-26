---
title: Registro de Devolução
description: Registro de Devolução
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Registro de Devolução {#return-registration-record}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Endpoints REST API {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>
 

## Descrição {#description}

Retorna o registro do código de registro contendo UUID do código de registro, código de registro e ID de dispositivo com hash. 

 

<div>


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Por exemplo:</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJCFK?format=xml | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante  </br>    (Componente de caminho)</br>2.  código de registro  </br>    (Componente de caminho) | GET | XML ou JSON contendo um código de registro e informações. Consulte esquema e amostra abaixo. | 200 |

{style=&quot;table-layout:auto&quot;}

</br>

| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| código de registro | O valor do código de registro que seria exibido no Dispositivo de transmissão (a ser inserido no fluxo de autenticação). |

</br>

## Esquema XML de Resposta {#response-xml-schema}

### Código de registro XSD

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>
```

| Nome do elemento | Descrição |
| --- | --- |
| id | UUID gerada pelo Serviço de Código de Registro |
| código | Código de Registro gerado pelo Serviço de Código de Registro |
| solicitante | ID do solicitante |
| mvpd | ID do MVPD |
| gerado | Carimbo de data e hora de criação do Código de Registro (em milissegundos desde 1° de janeiro de 1970 GMT) |
| expira | Carimbo de data e hora quando o código de registro expira (em milissegundos desde 1° de janeiro de 1970 GMT) |
| deviceId | ID de dispositivo exclusiva (ou token XSTS) |
| deviceType | Tipo de dispositivo |
| deviceUser | Usuário conectado ao dispositivo |
| appId | ID do aplicativo |
| appVersion | Versão do aplicativo |
| registrationURL | URL para o Aplicativo Web de Logon a ser exibido ao usuário final |

{style=&quot;table-layout:auto&quot;}

### Resposta de exemplo {#sample-response}

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```

[Voltar para Referência da API REST](http://tve.helpdocsonline.com/rest-api-reference)