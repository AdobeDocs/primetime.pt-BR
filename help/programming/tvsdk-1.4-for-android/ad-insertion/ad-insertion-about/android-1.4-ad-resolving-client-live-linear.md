---
description: Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.
seo-description: Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.
seo-title: Resolução e inserção de anúncios ao vivo/linear
title: Resolução e inserção de anúncios ao vivo/linear
uuid: a63c97c3-00c5-4dee-a42c-30b70e432b93
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Resolução e inserção de anúncio ao vivo/linear {#live-linear-ad-resolving-and-insertion}

Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.

Antes e durante a reprodução, o TVSDK resolve os anúncios conhecidos, substitui partes do conteúdo principal por pausas de anúncio da mesma duração e recompata a linha do tempo virtual, se necessário. As posições das quebras de anúncio são especificadas por pontos de sinalização definidos pelo manifesto.

O TVSDK insere anúncios das seguintes maneiras:

* **Pré-rolar**, no início do conteúdo.
* **No meio** do conteúdo.

O TVSDK aceita o intervalo do anúncio mesmo se a duração for maior ou menor do que a duração da substituição do ponto de sinalização. Por padrão, o TVSDK oferece suporte à indicação `#EXT-X-CUE` como um marcador de anúncio válido ao resolver e inserir anúncios. Esse marcador requer o campo de metadados `DURATION` em segundos e a ID exclusiva da dica. Por exemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Você pode definir e assinar dicas adicionais (tags).

Após os start de reprodução, o mecanismo de vídeo atualiza periodicamente o arquivo manifest. O TVSDK resolve quaisquer novos anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear que foi definido no manifesto. Depois que os anúncios são resolvidos e inseridos, o TVSDK calcula a linha do tempo virtual novamente e despacha um evento `TimelineItemsUpdatedEventListener.onTimelineUpdated`.
