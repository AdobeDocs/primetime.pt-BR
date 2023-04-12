---
title: Visualização gratuita do Temp Pass and Promotional Temp Pass
description: Visualização gratuita do Temp Pass and Promotional Temp Pass
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Visualização gratuita do Temp Pass and Promotional Temp Pass {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

Permite a criação de um token de autenticação para o Temp Pass and Promotional Temp Pass sem a necessidade de uma segunda tela.


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authentication/freepreview | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. requestor_id (Obrigatório)</br>    </br>2.  deviceId (Obrigatório)</br>    </br>3.  mso_id (Obrigatório)</br>    </br>4.  domain_name (Obrigatório)</br>    </br>5.  device_info/X-Device-Info (Obrigatório)</br>6.  deviceType</br>    </br>7.  deviceUser (obsoleto)</br>    </br>8.  appId (obsoleto)</br>    </br>9.  generic_data (opcional) | POST | A resposta bem-sucedida será 204 Sem conteúdo, indicando que o token foi criado com êxito e está pronto para uso para os fluxos de autenticação. | 204 - Sem conteúdo   </br>400 - Solicitação incorreta |

<div>


| Parâmetro de entrada | Descrição |
| --- | --- |
| requestor_id | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| mso_id | O ID do MVPD para o qual esta operação é válida. |
| nome_do_domínio | O nome de domínio para o qual um token será concedido. Isso está sendo comparado aos domínios do provedor de serviços quando um token de autorização está sendo concedido. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) ao usar a opção sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, AppleTV, Xbox etc.</br></br>Consulte [Benefícios do uso de parâmetros de tipo de dispositivo sem cliente ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Observação**: o device_info substituirá esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo.</br></br>**Observação**: se usado, deviceUser deve ter os mesmos valores de no [Criar código de registro](/help/authentication/registration-code-request.md) solicitação. |
| _appId_ | A ID/nome do aplicativo. </br></br>**Observação**: o device_info substitui esse parâmetro. Se usado, `appId` deve ter os mesmos valores de [Criar código de registro](/help/authentication/registration-code-request.md) solicitação. |
| generic_data | Usado para limitar o escopo do token para aprovação temporária promocional. |


### [Voltar para Referência da API REST](/help/authentication/rest-api-reference.md)
