---
description: A transcodificação just-in-time pode injetar metadados cronometrados da ID3 em anúncios criativos para facilitar o rastreamento de anúncios do lado do cliente.
title: Uso da transcodificação just-in-time para injetar tags de metadados de ID3
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Uso da transcodificação just-in-time para inserir tags de metadados de ID3 {#using-crs-to-inject-id-timed-metadata-tags}

Os CRS podem injetar metadados cronometrados de ID3 em anúncios criativos para facilitar o rastreamento de anúncios do lado do cliente.

O player do cliente lê os metadados de ID3 para ativar o rastreamento de anúncios com precisão de quadro.

>[!NOTE]
>
>ID3: Funções de injeção de metadados cronometradas somente para Safari/iOS.

## Fluxo de trabalho do CRS para injeção de ID3 {#workflow-for-crs-for-id3-injection}

Se o Ad Insertion do Primetime receber o `ptplayer=ios-mobileweb` , os pacotes de ID3 serão injetados na campanha de criação de anúncios transcodificados antes de serem carregados no CDN de armazenamento de anúncios apropriado.
