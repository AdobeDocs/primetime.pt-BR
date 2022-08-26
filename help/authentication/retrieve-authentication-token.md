---
title: Recuperar token de autenticação
description: Recuperar token de autenticação
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Recuperar token de autenticação {#retrieve-authentication-token}

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

Recupera o token de autenticação (AuthN).  

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn</br></br>Por exemplo:</br></br>&lt;sp_fqdn>/api/v1/tokens/authn | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (Obrigatório)</br>2.  deviceId (Obrigatório)</br>3.  device_info/X-Device-Info (Obrigatório)</br>4.  _deviceType_ (Obsoleto)</br>5.  _deviceUser_ (Obsoleto)</br>6.  _appId_ (Obsoleto) | GET | XML ou JSON contendo informações de autenticação ou detalhes do erro, se não tiver êxito. | 200 - Sucesso.  </br>404 - Token Não Encontrado  </br>410 - Token expirado |

{style=&quot;table-layout:auto&quot;}


| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br>Veja os detalhes completos em [Transmitindo informações de dispositivo e conexão](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>**Observação**: o device_info substitui esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo.</br></br>**Observação**: se usado, deviceUser deve ter os mesmos valores de no [Criar código de registro](http://tve.helpdocsonline.com/registration-code-request) solicitação. |
| _appId_ | A ID/nome do aplicativo. </br></br>**Observação**: o device_info substitui esse parâmetro. Se usado, `appId` deve ter os mesmos valores de [Criar código de registro](http://tve.helpdocsonline.com/registration-code-request) solicitação. |

{style=&quot;table-layout:auto&quot;}

</br>

### Resposta de exemplo {#response}

 

#### Sucesso

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authentication>
         <expires>1601114932000</expires>
         <userId>sampleUserId</userId>
         <mvpd>sampleMvpdId</mvpd>
         <requestor>sampleRequestor</requestor>
    </authentication>
```


**JSON:**

```JSON
    {
         "requestor": "sampleRequestor",
         "mvpd": "sampleMvpdId",
         "userId": "sampleUserId",
         "expires": "1601114932000"
    }
```

 

 

#### Token de autenticação não encontrado:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>404</status>
        <message>Not found</message>
    </error>
```

 
**JSON:**

```JSON
    {
        "status": 404,
        "message": "Not Found"
    }
```

[Voltar para a referência da API sem cliente](http://tve.helpdocsonline.com/clientless-api-reference)
