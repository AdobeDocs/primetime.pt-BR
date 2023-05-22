---
description: Para conteúdo dinâmico/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por um ad break com a mesma duração, para que a duração da linha do tempo permaneça a mesma.
title: Live/linear e resolução e inserção de anúncios
exl-id: b0fbdddf-8529-4f7a-aef2-1764320307f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Live/linear e resolução e inserção de anúncios{#live-linear-ad-resolving-and-insertion}

Para conteúdo dinâmico/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por um ad break com a mesma duração, para que a duração da linha do tempo permaneça a mesma.

Antes e durante a reprodução, o TVSDK resolve anúncios conhecidos, substitui partes do conteúdo principal por ad breaks com a mesma duração e recalcula a linha do tempo virtual, se necessário. As posições dos ad breaks são especificadas por pontos de sinalização definidos pelo manifesto.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, que está no início do conteúdo.
* **Durante a exibição**, que está no meio do conteúdo.

O TVSDK aceita o ad break mesmo se a duração for maior ou menor que a duração da substituição do ponto de sinalização. Por padrão, o TVSDK é compatível com o `#EXT-X-CUE` Indicar como um marcador de anúncio válido ao resolver e inserir anúncios. Este marcador requer o campo de metadados `DURATION` em segundos e o identificador exclusivo da indicação. Por exemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>Ao implementar uma `AdPolicySelector`, uma política diferente pode ser aplicada ao antes, durante e depois da exibição `AdBreakTimelineItem`s em `AdPolicyInfo`, que se baseia no tipo de `AdBreakTimelineItem`s. Por exemplo, você pode manter o conteúdo durante a exibição após sua reprodução, mas remover o conteúdo anterior à exibição após sua reprodução.

Depois que a reprodução começa, o mecanismo de vídeo atualiza periodicamente o arquivo de manifesto. O TVSDK resolve quaisquer novos anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear que foi definido no manifesto. Depois que os anúncios são resolvidos e inseridos, o TVSDK calcula a linha do tempo virtual novamente e envia um `TimelineEvent.TIMELINE_UPDATED` evento.
