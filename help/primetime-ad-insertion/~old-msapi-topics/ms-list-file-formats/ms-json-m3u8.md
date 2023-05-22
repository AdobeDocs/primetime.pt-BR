---
description: Se pttrackingmode=simple ou ptplayer=ios-mobileweb, o servidor de manifesto enviará de volta um arquivo formatado em JSON contendo Principal-M3U8, um URL que o cliente usará para solicitar o arquivo M3U8 que descreve o conteúdo.
title: Formato JSON para o URL da lista de reprodução de manifesto da variante
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Formato JSON para o URL da lista de reprodução de manifesto da variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Se `pttrackingmode=simple` ou `ptplayer=ios-mobileweb`, o servidor de manifesto envia de volta um arquivo formatado em JSON contendo Principal-M3U8, um URL que o cliente deve usar para solicitar o arquivo M3U8 que descreve o conteúdo.

Esse é o formato do arquivo JSON que contém a variável `Master-M3U8` URL.

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
