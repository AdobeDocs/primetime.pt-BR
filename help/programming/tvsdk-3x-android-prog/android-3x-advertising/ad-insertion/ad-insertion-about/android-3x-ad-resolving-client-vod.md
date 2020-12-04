---
description: Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-description: Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.
seo-title: Resolver e inserir anúncio VOD
title: Resolver e inserir anúncio VOD
uuid: b7124cab-441b-4b38-ac83-300ab9e5f9ec
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Resolver e inserir anúncios VOD {#resolve-and-insert-vod-ad}

Para conteúdo VOD (Video-on-demand), o TVSDK insere quebras de publicidade ao dividir as publicidades no conteúdo principal para que a duração da linha do tempo aumente.

Antes da reprodução, o TVSDK resolve os anúncios conhecidos, insere e quebra no conteúdo principal, conforme descrito por uma linha do tempo que é retornada pela decisão de anúncio do Adobe Primetime, e recompata a linha do tempo virtual, se necessário.

O TVSDK insere anúncios das seguintes maneiras:

* **Pré-rolar**, que é colocado antes do conteúdo.
* **Meia rolagem**, que está no meio do conteúdo.
* **Pós-rolagem**, que é colocada após o conteúdo.

>[!TIP]
>
>Após os start de reprodução, nenhuma alteração adicional pode ocorrer no conteúdo.

Os anúncios não podem ser:

* Inserido
* Excluído

   Por exemplo, não é possível excluir anúncios integrados do conteúdo para oferta de uma experiência sem anúncios.
* Substituído

   Por exemplo, não é possível substituir anúncios incorporados por anúncios direcionados.