---
title: Configurar o rastreamento de anúncios
description: Configuração do rastreamento de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Configurar o rastreamento de anúncios {#ser-up-ad-tracking}

A maioria dos anunciantes requer informações sobre quando, por quanto tempo e com que sucesso seus anúncios foram visualizados. O Ad Insertion do Primetime oferece suporte ao rastreamento de anúncios do lado do cliente, do lado do servidor e híbridos para fornecer flexibilidade na coleta dessas informações.

## Rastreamento de anúncios do lado do cliente com VMAP/JSON {#client-side-ad-tracking-vmap-json}

No rastreamento de anúncios do lado do cliente, o servidor envia ao cliente uma estrutura JSON, VMAP ou no manifesto especificando eventos de rastreamento e URLs, juntamente com a lista de reprodução compilada por anúncio.

Para ativar o rastreamento de anúncios do lado do cliente, especifique os seguintes parâmetros no [API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Definição de `pttrackingmode=simple` fará com que a solicitação inicial da API de inicialização retorne uma resposta JSON, em vez de um documento HLS ou DASH.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## Rastreamento de anúncios do lado do servidor {#server-side-ad-tracking}

Usando esse método, os dados de rastreamento do anúncio são calculados totalmente no lado do servidor. Isso é útil quando a atualização do aplicativo cliente não é viável. No entanto, o rastreamento de anúncios do lado do servidor pode não corresponder à atividade de reprodução do lado do cliente. Por exemplo, o servidor considera um anúncio a ser reproduzido após a entrega dos segmentos, mesmo que o usuário final não visualize o anúncio inteiro.

Para ativar o rastreamento de anúncios do lado do servidor, especifique o seguinte parâmetro no [API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

Consulte `pttrackingmode` seções de [API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

Todos os beacons de rastreamento de anúncios são enviados com os seguintes cabeçalhos HTTP de solicitação:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Esses valores contêm o agente do usuário do cliente/player e o endereço IP do cliente.

## Rastreamento de anúncios híbridos {#hybrid-ad-tracking}

Essa abordagem é como o rastreamento do lado do servidor, mas o aplicativo cliente também solicita cartões laterais do Primetime Ad Insertion para obter informações detalhadas de rastreamento. O rastreamento de anúncios híbridos pode fornecer anúncios não lineares, como sobreposições e companheiros para o aplicativo do cliente, enquanto ainda depende do Ad Insertion do Primetime para enviar URLs de rastreamento de anúncios individuais.
Para ativar o rastreamento de anúncios híbridos, consulte a `pttrackingmode` parâmetro no [API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
