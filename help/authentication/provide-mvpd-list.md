---
title: Fornecer Lista MVPD
description: Fornecer Lista MVPD
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Fornecer Lista MVPD {#provide-mvpd-list}

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

## Descrição {#description}

Retorna a lista de MVPDs configurados para o solicitante.

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>Por exemplo:</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Autenticação do Primetime | 1. Requerente</br>    (Componente de caminho)</br>_2.  deviceType (obsoleto)_ | GET | Lista de MVPDs que contém XML ou JSON. | 200 |

{style=&quot;table-layout:auto&quot;}


| Parâmetro de entrada | Descrição |
| --------------- | ------------------------------------------------------------- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| *deviceType* | Tipo de dispositivo. |

{style=&quot;table-layout:auto&quot;}

### Resposta de exemplo {#sample-response}

Igual à Resposta XML MVPD existente para o servlet /config

Observação: Todos os MVPDs configurados para usar o Platform SSO terão as seguintes propriedades extras em seus nós correspondentes (JSON/XML):

* **enablePlatformServices (booleano):** sinalizador indicando se esse MVPD está integrado via Platform SSO
* **boardingStatus (string):** sinalizador que indica se o MVPD suporta totalmente o Platform SSO (SUPORTADO) ou se o MVPD aparece apenas no seletor de plataforma (PICKER)
* **displayInPlatformPicker (booleano):** este MVPD deve aparecer no seletor de plataforma
* **platformMappingId (cadeia de caracteres):** o identificador deste MVPD conhecido pela plataforma
* **requiredMetadataFields (matriz de sequência):** os campos de metadados do usuário que devem estar disponíveis em um logon bem-sucedido


[Voltar para a referência da API sem cliente](http://tve.helpdocsonline.com/clientless-api-reference)
