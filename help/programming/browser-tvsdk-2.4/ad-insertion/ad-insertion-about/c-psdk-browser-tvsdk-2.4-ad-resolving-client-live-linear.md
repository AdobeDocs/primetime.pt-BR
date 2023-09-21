---
description: Para conteúdo dinâmico/linear, o TVSDK do navegador substitui uma parte do conteúdo do fluxo principal por um ad break com a mesma duração, para que a duração da linha do tempo permaneça a mesma.
title: Live/linear e resolução e inserção de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Live/linear e resolução e inserção de anúncios{#live-linear-ad-resolving-and-insertion}

Para conteúdo dinâmico/linear, o TVSDK do navegador substitui uma parte do conteúdo do fluxo principal por um ad break com a mesma duração, para que a duração da linha do tempo permaneça a mesma.

Antes e durante a reprodução, o TVSDK do navegador resolve anúncios conhecidos, substitui partes do conteúdo principal por ad breaks com a mesma duração e recalcula a linha do tempo virtual, se necessário. As posições dos ad breaks são especificadas por pontos de sinalização definidos pelo manifesto.

O TVSDK do navegador insere anúncios das seguintes maneiras:

* **Antes da exibição**, que está no início do conteúdo.

O TVSDK do navegador aceita o ad break mesmo se a duração for maior ou menor que a duração da substituição do ponto de sinalização. Por padrão, o TVSDK do navegador é compatível com o `#EXT-X-CUE` Indicar como um marcador de anúncio válido ao resolver e inserir anúncios. Este marcador requer o campo de metadados `DURATION` em segundos e o identificador exclusivo da indicação. Por exemplo:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

É possível definir e assinar dicas adicionais (tags).

Depois que a reprodução começa, o mecanismo de vídeo atualiza periodicamente o arquivo de manifesto. O TVSDK do navegador resolve quaisquer novos anúncios e insere os anúncios quando um ponto de sinalização é encontrado no fluxo ao vivo ou linear que foi definido no manifesto. Depois que os anúncios são resolvidos e inseridos, o TVSDK do navegador calcula a linha do tempo virtual novamente e envia um `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` evento.

>[!TIP]
>
>Para transmissões ao vivo, o TVSDK do navegador é compatível apenas com anúncios MP4 e HLS precedentes e intermediários.
