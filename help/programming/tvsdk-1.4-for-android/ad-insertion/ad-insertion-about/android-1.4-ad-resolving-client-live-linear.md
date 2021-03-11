---
description: Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por um ad break da mesma duração, para que a duração da linha do tempo permaneça a mesma.
title: Resolução e inserção de anúncios em tempo real/linear
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Resolução e inserção de anúncio ao vivo/linear {#live-linear-ad-resolving-and-insertion}

Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por um ad break da mesma duração, para que a duração da linha do tempo permaneça a mesma.

Antes e durante a reprodução, o TVSDK resolve anúncios conhecidos, substitui partes do conteúdo principal por intervalos de anúncios da mesma duração e recalcula a linha do tempo virtual, se necessário. As posições dos ad breaks são especificadas por pontos de sinalização definidos pelo manifesto.

O TVSDK insere anúncios das seguintes maneiras:

* **Antes da exibição**, no início do conteúdo.
* **Meio**, no meio do conteúdo.

O TVSDK aceita o ad break, mesmo se a duração for maior ou menor que a duração do ponto de sinalização de substituição. Por padrão, o TVSDK oferece suporte à sinalização `#EXT-X-CUE` como um marcador de anúncio válido ao resolver e inserir anúncios. Esse marcador requer o campo de metadados `DURATION` em segundos e a ID exclusiva da sinalização. Por exemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Você pode definir e assinar dicas adicionais (tags).

Após o início da reprodução, o mecanismo de vídeo atualiza periodicamente o arquivo manifest. O TVSDK resolve quaisquer novos anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear que foi definido no manifesto. Depois que os anúncios são resolvidos e inseridos, o TVSDK calcula a linha do tempo virtual novamente e despacha um evento `TimelineItemsUpdatedEventListener.onTimelineUpdated`.
