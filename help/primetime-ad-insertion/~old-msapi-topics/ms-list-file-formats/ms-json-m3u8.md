---
description: Se pttrackingmode=simple ou ptplayer=ios-mobileweb, o servidor de manifesto envia um arquivo formatado JSON contendo Principal-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 descrevendo o conteúdo.
title: Formato JSON para URL para a lista de reprodução de manifesto da variante de solicitação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Formato JSON para URL para solicitação de lista de reprodução de manifesto de variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Se `pttrackingmode=simple` ou `ptplayer=ios-mobileweb`, o servidor de manifesto envia um arquivo formatado JSON contendo Principal-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 descrevendo o conteúdo.

Este é o formato do arquivo JSON que contém a URL `Master-M3U8`.

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
