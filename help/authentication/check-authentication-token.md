---
title: Verificar Token de Autenticação
description: Verificar Token de Autenticação
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Verificar Token de Autenticação {#check-authentication-token}

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

Indica se o dispositivo tem um token de autenticação não expirado.

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/checkauthn | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (Obrigatório)</br>2.  deviceId (Obrigatório)</br>3.  device_info/X-Device-Info (Obrigatório)</br>4.  _deviceType_ </br>5.  _deviceUser_ (Obsoleto)</br>6.  _appId_ (Obsoleto) | GET | XML ou JSON contendo detalhes do erro, se não tiver êxito. | 200 - Sucesso   </br>403 - Sem sucesso |

{style=&quot;table-layout:auto&quot;}


| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e às limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br>Veja os detalhes completos em [Transmitindo informações de dispositivo e conexão](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) ao usar a opção sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, AppleTV, Xbox etc.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**Observação**: o device_info substituirá esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo. |
| _appId_ | A ID/nome do aplicativo.</br>**Observação**: o device_info substitui esse parâmetro. |

{style=&quot;table-layout:auto&quot;}


## Resposta (se não tiver êxito) {#response}

```JSON
    <error>
      <status>403</status>
      <message>Authentication token expired</message>
    </error>
```

### [Voltar para Referência da API REST](http://tve.helpdocsonline.com/rest-api-reference)
