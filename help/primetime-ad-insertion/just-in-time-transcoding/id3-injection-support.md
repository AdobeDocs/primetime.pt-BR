---
description: A transcodificação just-in-time pode injetar metadados ID3 cronometrados em anúncios para facilitar o rastreamento de anúncios pelo lado do cliente.
title: Usar transcodificação just-in-time para injetar tags de metadados cronometradas ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Usar a transcodificação just-in-time para inserir as tags de metadados cronometradas ID3 {#using-crs-to-inject-id-timed-metadata-tags}

O CRS pode inserir metadados ID3 cronometrados em anúncios para facilitar o rastreamento de anúncios do cliente.

O reprodutor do cliente lê os metadados ID3 para ativar o rastreamento de anúncios preciso de quadros.

>[!NOTE]
>
>ID3 atingiu as funções de injeção de metadados somente para Safari/iOS.

## Fluxo de trabalho do CRS para Injeção de ID3 {#workflow-for-crs-for-id3-injection}

Se o Primetime Ad Insertion receber o parâmetro `ptplayer=ios-mobileweb`, ele injetará pacotes ID3 no anúncio transcodificado antes de fazer upload para o CDN de armazenamento de anúncios apropriado.
