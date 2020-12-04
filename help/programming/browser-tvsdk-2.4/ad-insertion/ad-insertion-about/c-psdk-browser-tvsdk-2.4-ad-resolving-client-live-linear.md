---
description: Para conteúdo ao vivo/linear, o TVSDK do navegador substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.
seo-description: Para conteúdo ao vivo/linear, o TVSDK do navegador substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.
seo-title: Resolução e inserção de anúncios ao vivo/linear
title: Resolução e inserção de anúncios ao vivo/linear
uuid: 18c6733a-e827-4b1c-9cd5-796d57cbdb05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# Resolução e inserção de anúncios ao vivo/linear{#live-linear-ad-resolving-and-insertion}

Para conteúdo ao vivo/linear, o TVSDK do navegador substitui uma parte do conteúdo do fluxo principal por uma quebra de anúncio da mesma duração, de modo que a duração da linha do tempo permaneça a mesma.

Antes e durante a reprodução, o TVSDK do navegador resolve anúncios conhecidos, substitui partes do conteúdo principal por quebras de anúncios da mesma duração e recompata a linha do tempo virtual, se necessário. As posições das quebras de anúncio são especificadas por pontos de sinalização definidos pelo manifesto.

O TVSDK do navegador insere anúncios das seguintes maneiras:

* **Pré-rolar**, que está no início do conteúdo.

O TVSDK do navegador aceita o intervalo do anúncio mesmo se a duração for maior ou menor do que a duração da substituição do ponto de sinalização. Por padrão, o TVSDK do navegador suporta a indicação `#EXT-X-CUE` como um marcador de anúncio válido ao resolver e inserir anúncios. Esse marcador requer o campo de metadados `DURATION` em segundos e a ID exclusiva da dica. Por exemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Você pode definir e assinar dicas adicionais (tags).

Após os start de reprodução, o mecanismo de vídeo atualiza periodicamente o arquivo manifest. O TVSDK do navegador resolve quaisquer novos anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear que foi definido no manifesto. Depois que os anúncios são resolvidos e inseridos, o TVSDK do navegador calcula a linha do tempo virtual novamente e despacha um evento `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.

>[!TIP]
>
>Para fluxos ao vivo, o TVSDK do navegador suporta apenas anúncios de registro e pré-rolagem MP4 e HLS.

