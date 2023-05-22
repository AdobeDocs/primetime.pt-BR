---
description: A transcodificação just-in-time pode injetar metadados cronometrados da ID3 em anúncios criativos para facilitar o rastreamento de anúncios do lado do cliente.
title: Uso da transcodificação just-in-time para injetar tags de metadados de ID3
exl-id: 6171223a-71f9-45a2-a3f5-7ede4a9b101a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
