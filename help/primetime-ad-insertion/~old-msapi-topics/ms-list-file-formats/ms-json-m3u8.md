---
description: Se pttrackingmode=simple ou ptplayer=ios-mobileweb, o servidor manifest envia um arquivo formatado JSON contendo Principal-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 que descreve o conteúdo.
seo-description: Se pttrackingmode=simple ou ptplayer=ios-mobileweb, o servidor manifest envia um arquivo formatado JSON contendo Principal-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 que descreve o conteúdo.
seo-title: Formato JSON para URL para solicitação de lista de reprodução de manifesto variante
title: Formato JSON para URL para solicitação de lista de reprodução de manifesto variante
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Formato JSON para URL para solicitação de lista de reprodução de manifesto de variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Se `pttrackingmode=simple` ou `ptplayer=ios-mobileweb`, o servidor manifest enviará um arquivo formatado JSON contendo Principal-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 que descreve o conteúdo.

Este é o formato do arquivo JSON que contém o URL `Master-M3U8`.

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
