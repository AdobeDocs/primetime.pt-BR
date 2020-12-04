---
description: O CRS pode injetar metadados cronometrados ID3 no formato HLS e criar anúncios para facilitar o rastreamento de anúncios do cliente.
seo-description: O CRS pode injetar metadados cronometrados ID3 no formato HLS e criar anúncios para facilitar o rastreamento de anúncios do cliente.
seo-title: Uso do CRS para injetar tags de metadados cronometradas ID3
title: Uso do CRS para injetar tags de metadados cronometradas ID3
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Usando o CRS para injetar tags de metadados cronometradas ID3 {#using-crs-to-inject-id-timed-metadata-tags}

O CRS pode injetar metadados cronometrados ID3 no formato HLS e criar anúncios para facilitar o rastreamento de anúncios do cliente.

O player do cliente lê os metadados ID3 para permitir o rastreamento de anúncios com precisão de quadros.

>[!NOTE]
>
>A injeção de metadados cronometrados ID3 funciona somente no Safari no iOS.

## Fluxo de trabalho do CRS para a Injeção de ID3 {#workflow-for-crs-for-id3-injection}

O fluxo de trabalho da injeção de ID3 é o mesmo que em [Workflows detalhados para o reempacotamento JIT.](../creative-repackaging-service/jit-repackage.md) Se o servidor manifest receber o  `ptplayer=ios-mobileweb` parâmetro, ele instrui o CRS a injetar pacotes ID3 no anúncio transcodificado antes de carregá-lo no servidor CDN.

>[!NOTE]
>
>Em uma configuração de vários CDN, o servidor manifest usa o parâmetro `ptcdn` no URL de inicialização para identificar o servidor CDN para carregar o anúncio criativo.