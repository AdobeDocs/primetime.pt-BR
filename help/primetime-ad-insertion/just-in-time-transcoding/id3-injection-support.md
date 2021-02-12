---
description: A transcodificação just-in-time pode injetar metadados cronometrados ID3 em anúncios para facilitar o rastreamento de anúncios do cliente.
seo-description: A transcodificação just-in-time pode injetar metadados cronometrados ID3 no formato HLS e criar para facilitar o rastreamento de anúncios do cliente.
seo-title: Usando transcodificação just-in-time para injetar tags de metadados cronometradas ID3
title: Usando transcodificação just-in-time para injetar tags de metadados cronometradas ID3
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Usando transcodificação just-in-time para injetar tags de metadados cronometradas ID3 {#using-crs-to-inject-id-timed-metadata-tags}

O CRS pode injetar metadados cronometrados ID3 em anúncios para facilitar o rastreamento de anúncios do cliente.

O player do cliente lê os metadados ID3 para permitir o rastreamento de anúncios com precisão de quadros.

>[!NOTE]
>
>ID3 atingiu o tempo de funções de injeção de metadados somente para Safari/iOS.

## Fluxo de trabalho do CRS para a Injeção de ID3 {#workflow-for-crs-for-id3-injection}

Se o Primetime Ad Insertion receber o parâmetro `ptplayer=ios-mobileweb`, ele injetará pacotes ID3 no anúncio codificado e no anúncio, antes de fazer upload para o CDN armazenamento de anúncio apropriado.
