---
title: Página de registro
description: Página de registro
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Página de registro {#registration-page}

## Endpoints REST API {#clientless-endpoints}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

&lt;reggie_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Descrição {#create-reg-code-svc}

Retorna o código de registro gerado aleatoriamente e o URI da página de logon.

| Endpoint | Chamado  </br>Por | Entrada   </br>Parâmetro | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestor}/regcode</br>Por exemplo:</br>REGGIE_FQDN/reggie/v1/sampleRequestorId/regcode | Aplicativo de transmissão</br>ou</br>Serviço de programador | 1. solicitante  </br>    (Componente de caminho)</br>2.  deviceId (Hash)   </br>    (Obrigatório)</br>3.  device_info/X-Device-Info (Obrigatório)</br>4.  mvpd (Opcional)</br>5.  ttl (Opcional)</br>6.  _deviceType_</br> 7.  _deviceUser_ (Obsoleto)</br>8.  _appId_ (Obsoleto) | POST | XML ou JSON contendo um código de registro e informações ou detalhes do erro, se não tiver êxito. Consulte esquemas e amostras abaixo. | 201º |

{style=&quot;table-layout:auto&quot;}

| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| device_info/</br>X-Device-Info | Informações do dispositivo de transmissão.</br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br>Veja os detalhes completos em [Transmitindo informações de dispositivo e conexão](http://tve.helpdocsonline.com/passing-device-information). |
| mvpd | A ID MVPD para a qual esta operação é válida. |
| ttl | Por quanto tempo esse código de registro deve estar ativo em segundos.</br>**Observação**: O valor máximo permitido para ttl é 36000 segundos (10 horas). Valores mais altos resultam em uma resposta HTTP 400 (solicitação inválida). If `ttl` for deixado em branco, a autenticação do Primetime definirá um valor padrão de 30 minutos. |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) ao usar a opção sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, AppleTV, Xbox etc.</br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**Observação**: o device_info substituirá esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo. |
| _appId_ | A ID/nome do aplicativo. </br>**Observação**: o device_info substitui esse parâmetro. |

{style=&quot;table-layout:auto&quot;}


>[!CAUTION]
>
>**Endereço IP do dispositivo de transmissão**
></br>
>Para implementações de cliente para servidor, o Endereço IP do dispositivo de transmissão é enviado implicitamente com esta chamada.  Para implementações de servidor para servidor, em que a variável **regcode** A chamada é feita como o Serviço do programador e não como o Dispositivo de transmissão, o seguinte cabeçalho é necessário para passar o Endereço IP do Dispositivo de transmissão:
>
>
>
```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>em que `<streaming\_device\_ip>` é o endereço IP público do Dispositivo de transmissão.
></br></br>
>Exemplo :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1</br>X-Forwarded-For:203.45.101.20
>```
</br>

### Esquema XML de Resposta {#xml-schema}


#### Código de registro XSD {#registration-code-xsd}

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

 </br>

| Nome do elemento | Descrição |
| --------------- | ------------------------------------------------------------------------------------ |
| id | UUID gerada pelo Serviço de Código de Registro |
| código | Código de Registro gerado pelo Serviço de Código de Registro |
| solicitante | ID do solicitante |
| mvpd | ID Mvpd |
| gerado | Carimbo de data e hora de criação do Código de Registro (em milissegundos desde 1° de janeiro de 1970 GMT) |
| expira | Carimbo de data e hora quando o código de registro expira (em milissegundos desde 1° de janeiro de 1970 GMT) |
| deviceId | ID de dispositivo exclusiva (ou token XSTS) |
| deviceType | Tipo de dispositivo |
| deviceUser | Usuário conectado ao dispositivo |
| appId | ID do aplicativo |
| appVersion | Versão do aplicativo |
| registrationURL | URL para o Aplicativo Web de Logon a ser exibido ao usuário final |

{style=&quot;table-layout:auto&quot;}
 </br>

 

### Mensagem de erro XSD  {#error-message}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="rest.pass.adobe.com"
               targetNamespace="rest.pass.adobe.com"
               attributeFormDefault="unqualified"
               elementFormDefault="unqualified">
        <xs:element name="error">
            <xs:complexType>
                <xs:all>
                    <xs:element name="status" type="xs:int" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="message" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="details" type="xs:string" minOccurs="0" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
    </xs:schema>
```
 

### Resposta de exemplo {#sample-response}

**XML:**

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
 
**JSON:**

```JSON
    {
        "id": "678f9fea-9d364b29-246c-488f-b97e-298566d1b9e0",
        "code": "D4BDU2W",
        "requestor": "sampleRequestorId",
        "mvpd": "sampleMvpdId",
        "generated": 1348039555877,
        "expires": 1348043155877,
        "info": {
            "deviceId": "dGhpc0l.kQUR1bW15RGV2.aWNlSWQ=",
            "deviceType": "xboxOne",
            "deviceUser": "JD",
            "appId": "2345",
            "appVersion": "2.0",
            "registrationURL": "http://loginwebapp.com"
        }
    }
```

[Voltar para Referência da API REST](http://tve.helpdocsonline.com/rest-api-reference)
