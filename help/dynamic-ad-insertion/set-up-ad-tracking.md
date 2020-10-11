---
title: Configurar o rastreamento de anúncios
description: Configuração do rastreamento de anúncios
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Configurar o rastreamento de anúncios {#ser-up-ad-tracking}

A maioria dos anunciantes requer informações sobre quando, por quanto tempo e com que sucesso seus anúncios foram exibidos. O Primetime Ad Insertion oferece suporte ao rastreamento de anúncios do lado do cliente, do lado do servidor e híbrido para oferecer flexibilidade na coleta dessas informações.

## Rastreamento de anúncios do cliente com VMAP/JSON {#client-side-ad-tracking-vmap-json}

No rastreamento de anúncios do cliente, o servidor envia ao cliente uma estrutura JSON, VMAP ou in-manifest que especifica eventos de rastreamento e URLs junto com a lista de reprodução de anúncios.

Para ativar o rastreamento de anúncios do cliente, especifique os seguintes parâmetros na API [do](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)Bootstrap.

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>A configuração do `pttrackingmode=simple` fará com que a solicitação da API de inicialização retorne uma resposta JSON, em vez de um documento HLS ou DASH.

Para obter mais informações sobre `pttrackingmode`, `pttrackingversion` formatos, consulte Referência [da API: Parâmetros](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)do query do servidor manifest.

## Rastreamento de anúncios do servidor {#server-side-ad-tracking}

Usando esse método, os dados de rastreamento de anúncio são calculados totalmente no lado do servidor. Isso é útil quando a atualização do aplicativo cliente não é viável. No entanto, o rastreamento de anúncios do lado do servidor pode não corresponder à atividade de reprodução do lado do cliente. Por exemplo, o servidor considera que um anúncio deve ser reproduzido após a entrega dos segmentos, mesmo se o usuário final não visualização todo o anúncio.

Para ativar o rastreamento de anúncios do lado do servidor, especifique o seguinte parâmetro na API [do](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)Bootstrap.

`pttrackingmode=sstm`

Consulte `pttrackingmode` as seções da API [do](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)Bootstrap.

Todos os beacons de rastreamento de anúncios são enviados com os seguintes cabeçalhos de Solicitação HTTP:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Esses valores contêm o cliente/agente do usuário do player e o endereço IP do cliente.

## Rastreamento de anúncios híbridos {#hybrid-ad-tracking}

Essa abordagem é semelhante ao rastreamento do lado do servidor, mas o aplicativo cliente também solicita dispositivos auxiliares do Primetime Ad Insertion para obter informações detalhadas sobre o rastreamento. O rastreamento de anúncios híbridos pode fornecer anúncios não lineares, como sobreposições e companheiros, para o aplicativo cliente, e ainda depender do Primetime Ad Insertion para enviar URLs de rastreamento de anúncios individuais.
Para ativar o rastreamento de anúncios híbridos, consulte o `pttrackingmode` parâmetro na API [do](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)Bootstrap.
