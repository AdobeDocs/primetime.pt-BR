---
description: Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.
seo-description: Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.
seo-title: Resolução e inserção de anúncios ao vivo/linear
title: Resolução e inserção de anúncios ao vivo/linear
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Resolução e inserção de anúncios ao vivo/linear{#live-linear-ad-resolving-and-insertion}

Para conteúdo ao vivo/linear, o TVSDK substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.

Antes e durante a reprodução, o TVSDK resolve os anúncios conhecidos, substitui partes do conteúdo principal por pausas de anúncio da mesma duração e recompata a linha do tempo virtual, se necessário. As posições das quebras de anúncio são especificadas por pontos de sinalização definidos pelo manifesto.

O TVSDK insere anúncios das seguintes maneiras:

* **Pré-rolar**, que está no início do conteúdo.
* **Meia rolagem**, que está no meio do conteúdo.

O TVSDK aceita o intervalo do anúncio mesmo se a duração for maior ou menor do que a duração da substituição do ponto de sinalização. Por padrão, o TVSDK suporta a `#EXT-X-CUE` indicação como um marcador de anúncio válido ao resolver e inserir anúncios. Esse marcador requer o campo de metadados `DURATION` em segundos e a ID exclusiva da dica. Por exemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>Ao implementar um cliente `AdPolicySelector`, uma política diferente pode ser dada para pre-roll, mid-roll e post-roll `AdBreakTimelineItem`s in `AdPolicyInfo`, com base no tipo de `AdBreakTimelineItem`s. Por exemplo, você pode manter o conteúdo intermediário após a reprodução, mas remover o conteúdo anterior após a reprodução.

Após o início da reprodução, o mecanismo de vídeo atualiza periodicamente o arquivo manifest. O TVSDK resolve quaisquer novos anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear que foi definido no manifesto. Depois que os anúncios são resolvidos e inseridos, o TVSDK calcula a linha do tempo virtual novamente e despacha um `TimelineEvent.TIMELINE_UPDATED` evento.
