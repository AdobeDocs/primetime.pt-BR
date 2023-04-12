---
title: Obter token de mídia curta
description: obter token de mídia curto
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Obter token de mídia curta {#obtain-short-media-token}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Endpoints REST API {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produção - [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* Estágios - [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produção - [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* Estágios - [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

</br>

## Descrição {#description}

Obtém o Token de Mídia Curta.  

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/mediatoken</br></br>  ou</br></br>&lt;sp_fqdn>/api/v1/tokens/media</br></br>Por exemplo:</br></br>&lt;sp_fqdn>/api/v1/tokens/media | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (Obrigatório)</br>2.  deviceId (Obrigatório)</br>3.  recurso (Obrigatório)</br>4.  device_info/X-Device-Info (Obrigatório)</br>5.  _deviceType_</br> 6.  _deviceUser_ (Obsoleto)</br>7.  _appId_ (Obsoleto) | GET | XML ou JSON contendo um token de mídia codificado Base64 ou detalhes do erro se não tiver êxito. | 200 - Sucesso  </br>403 - Sem sucesso |

{style="table-layout:auto"}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>

| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| recurso | Uma string que contém um resourceId (ou fragmento MRSS), identifica o conteúdo solicitado por um usuário e é reconhecido pelos pontos finais de autorização MVPD. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br>Veja os detalhes completos em [Transmitindo informações de dispositivo e conexão](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo]/(help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) ao usar Clientless, para que diferentes tipos de análise possam ser executados. Por exemplo, Roku, AppleTV e Xbox.</br></br>Consulte [Benefícios do uso do parâmetro de tipo de dispositivo sem cliente ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Observação**: o device_info substituirá esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo.</br></br>**Observação**: Se for usado, deviceUser deve ter os mesmos valores do [Criar código de registro](/help/authentication/registration-code-request.md) solicitação. |
| _appId_ | A ID/nome do aplicativo. </br></br>**Observação**: o device_info substitui esse parâmetro. Se usado, `appId` deve ter os mesmos valores de [Criar código de registro](/help/authentication/registration-code-request.md) solicitação. |

{style="table-layout:auto"}

### Resposta de exemplo {#response}

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <play>
        <expires>1348649569000</expires>
        <mvpdId>sampleMvpdId</mvpdId>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <serializedToken>PHNpZ25hdH[...]</serializedToken>
        <userId>sampleScrambledUserId</userId>
    </play>
```



**JSON:**

```JSON
    {
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348649614000",
        "serializedToken": "PHNpZ25hdH[...]",
        "userId": "sampleScrambledUserId",
        "mvpdId": "sampleMvpdId"
    }
```

 

### Compatibilidade da Biblioteca de verificação de mídia

O campo `serializedToken` da chamada &quot;Obter token de mídia curta&quot;, há um token codificado Base64 que pode ser verificado na Biblioteca de verificação do Adobe Medium.
