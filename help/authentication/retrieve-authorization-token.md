---
title: Recuperar token de autorização
description: Recuperar token de autorização
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Recuperar token de autorização {#retrieve-authorization-token}

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

Recupera o token de autorização (AuthZ).  


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authz</br></br>Por exemplo:</br></br>&lt;sp_fqdn>/api/v1/tokens/authz | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (Obrigatório)</br>2.  deviceId (Obrigatório)</br>3.  recurso (Obrigatório)</br>4.  device_info/X-Device-Info (Obrigatório)</br>5.  _deviceType_</br> 6.  _deviceUser_ (Obsoleto)</br>7.  _appId_ (Obsoleto) | GET | 1. Sucesso</br>2.  Token de autenticação  </br>    não encontrado ou expirou:   </br>    Motivo da explicação XML  </br>    token de autenticação não encontrado</br>3.  Token de autorização  </br>    não encontrado:  </br>    Explicação do XML</br>4.  Token de autorização  </br>    expirado:  </br>    Explicação do XML | 200 - Sucesso  </br>412 - No AuthN</br></br>404 - No AuthZ</br></br>410 - AuthZ Expirado |

{style="table-layout:auto"}

</br>

| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| recurso | Uma string que contém um resourceId (ou fragmento MRSS), identifica o conteúdo solicitado por um usuário e é reconhecido pelos pontos finais de autorização MVPD. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) ao usar Clientless, para que diferentes tipos de análise possam ser executados, por exemplo, Roku, AppleTV e Xbox.</br></br>Consulte [Benefícios do uso do parâmetro de tipo de dispositivo sem cliente nas métricas de transmissão ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Observação**: o device_info substituirá esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo. |
| _appId_ | A ID/nome do aplicativo. </br></br>**Observação**: o device_info substitui esse parâmetro. |

{style="table-layout:auto"}


### Resposta de exemplo {#response}

 

#### Sucesso

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
        <expires>1348148289000</expires>
        <mvpd>sampleMvpdId</mvpd>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <proxyMvpd>sampleProxyMvpdId</proxyMvpd>
    </authorization>
```

 

**JSON:**

```JSON
    {
        "mvpd": "sampleMvpdId",
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348148289000",
        "proxyMvpd": "sampleProxyMvpdId"
    }
```

 </br>


#### Token de autenticação não encontrado ou expirado:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>412</status>
        <message>User not authenticated</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 412,
        "message": "User not authenticated",
        "details": null
    }
```

</br>
 

#### Token de autorização não encontrado:

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
        "message": "Not Found",
        "details": null
    }
```

</br>

 

#### Token de autorização expirado:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>410</status>
        <message>Gone</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 410,
        "message": "Gone",
        "details": null
    }
```
