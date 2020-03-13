---
description: Se pttrackingmode=simple ou ptplayer=ios-mobileweb, o servidor manifest envia um arquivo formatado em JSON contendo Master-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 que descreve o conteúdo.
seo-description: Se pttrackingmode=simple ou ptplayer=ios-mobileweb, o servidor manifest envia um arquivo formatado em JSON contendo Master-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 que descreve o conteúdo.
seo-title: Formato JSON para URL para solicitação de lista de reprodução de manifesto variante
title: Formato JSON para URL para solicitação de lista de reprodução de manifesto variante
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Formato JSON para URL para solicitação de lista de reprodução de manifesto variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Se `pttrackingmode=simple` ou `ptplayer=ios-mobileweb`, o servidor manifest envia um arquivo formatado JSON contendo Master-M3U8, um URL para o cliente usar para solicitar o arquivo M3U8 que descreve o conteúdo.

Esse é o formato do arquivo JSON que contém o `Master-M3U8` URL.

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
