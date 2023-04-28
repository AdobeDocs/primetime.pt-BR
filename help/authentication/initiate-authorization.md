---
title: Iniciar Autorização
description: Iniciar Autorização
exl-id: 2f8a5499-e94f-40dd-9fb0-aac8e080de66
source-git-commit: 5e775238f0e894f887be4c188903bdb04524c57a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Iniciar Autorização {#initiate-authorization}

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

Obtém a resposta de autorização. 

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authorized | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (Obrigatório)</br>2.  deviceId (Obrigatório)</br>3.  recurso (Obrigatório)</br>4.  device_info/X-Device-Info (Obrigatório)</br>5.  _deviceType_</br> 6.  _deviceUser_ (Obsoleto)</br>7.  _appId_ (Obsoleto)</br>8.  parâmetros adicionais (Opcional) | GET | XML ou JSON contendo detalhes de autorização ou detalhes do erro, se não tiver êxito. Veja as amostras abaixo. | 200 - Sucesso  </br>403 - Sem sucesso |

{style="table-layout:auto"}

</br>


| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| recurso | Uma string que contém um resourceId (ou fragmento MRSS), identifica o conteúdo solicitado por um usuário e é reconhecido pelos pontos finais de autorização MVPD. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) ao usar a opção sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, AppleTV, Xbox etc.</br></br>Consulte [Benefícios do parâmetro de tipo de dispositivo sem cliente nas métricas de transmissão ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Observação**: o device_info substituirá esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo. |
| _appId_ | A ID/nome do aplicativo. </br></br>**Observação**: o device_info substitui esse parâmetro. |
| parâmetros adicionais | A chamada também pode conter parâmetros opcionais que permitem outras funcionalidades como:</br></br>* generic_data - permite o uso de [TempPass Promocionais](/help/authentication/promotional-temp-pass.md)</br></br>Exemplo: `generic_data=("email":"email@domain.com")` |

{style="table-layout:auto"}

>[!CAUTION]
>
>**Endereço IP do dispositivo de transmissão**</br>
>Para implementações de cliente para servidor, o Endereço IP do dispositivo de transmissão é enviado implicitamente com esta chamada.  Para implementações de servidor para servidor, em que a variável **regcode** A chamada é feita pelo Serviço do programador e não pelo Dispositivo de transmissão, o seguinte cabeçalho é necessário para passar o Endereço IP do Dispositivo de transmissão:</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>em que `<streaming\_device\_ip>` é o endereço IP público do Dispositivo de transmissão.</br></br>
>Exemplo :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### Resposta de exemplo {#sample-response}

* **Caso 1: Sucesso**

</br>
  * **XML:**
  </br>

    &quot;XML
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot; standalone=&quot;yes&quot;?>
    &lt;authorization>
    &lt;expires>1348148289000&lt;/expires>
    &lt;mvpd>sampleMvpdId&lt;/mvpd>
    &lt;requestor>sampleRequestorId&lt;/requestor>
    &lt;resource>sampleResourceId&lt;/resource>
    &lt;/authorization>
    &quot;



* **JSON:**

   ```JSON
   {
     "mvpd": "sampleMvpdId",
     "resource": "sampleResourceId",
     "requestor": "sampleRequestorId",
     "expires": "1348148289000"
   }
   ```

>[!IMPORTANT]
>
>Quando a resposta vem de um MVPD do Proxy, ele pode incluir um elemento adicional chamado `proxyMvpd`. 

 

* **Caso 2: Autorização negada**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```
