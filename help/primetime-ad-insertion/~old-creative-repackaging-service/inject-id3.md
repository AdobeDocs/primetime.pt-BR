---
description: O CRS pode inserir metadados ID3 cronometrados no formato HLS e criar anúncios para facilitar o rastreamento de anúncios do cliente.
title: Uso do CRS para inserir tags de metadados cronometradas ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Uso do CRS para Inserir ID3 Tags de metadados cronometrados {#using-crs-to-inject-id-timed-metadata-tags}

O CRS pode inserir metadados ID3 cronometrados no formato HLS e criar anúncios para facilitar o rastreamento de anúncios do cliente.

O reprodutor do cliente lê os metadados ID3 para ativar o rastreamento de anúncios preciso de quadros.

>[!NOTE]
>
>A injeção de metadados cronometrados ID3 funciona somente no Safari no iOS.

## Fluxo de trabalho do CRS para Injeção de ID3 {#workflow-for-crs-for-id3-injection}

O fluxo de trabalho para a injeção de ID3 é o mesmo que em [Fluxos de trabalho detalhados para reempacotamento de JIT.](../~old-creative-repackaging-service/jit-repackage.md) Se o servidor de manifesto receber o  `ptplayer=ios-mobileweb` parâmetro , ele instrui o CRS a injetar pacotes ID3 no anúncio transcodificado antes de carregá-lo no servidor CDN.

>[!NOTE]
>
>Em uma configuração de vários CDN, o servidor de manifesto usa o parâmetro `ptcdn` no URL de inicialização para identificar o servidor CDN para fazer upload do anúncio criativo.