---
description: O CRS pode inserir metadados cronometrados de ID3 em anúncios no formato HLS e criações para facilitar o rastreamento de anúncios do lado do cliente.
title: Uso do CRS para injetar tags de metadados de ID3
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Uso do CRS para injetar tags de metadados de ID3 {#using-crs-to-inject-id-timed-metadata-tags}

O CRS pode inserir metadados cronometrados de ID3 em anúncios no formato HLS e criações para facilitar o rastreamento de anúncios do lado do cliente.

O player do cliente lê os metadados de ID3 para ativar o rastreamento de anúncios com precisão de quadro.

>[!NOTE]
>
>A injeção de metadados cronometrados da ID3 funciona somente no Safari no iOS.

## Fluxo de trabalho do CRS para injeção de ID3 {#workflow-for-crs-for-id3-injection}

O workflow para injeção de ID3 é o mesmo que em [Fluxos de Trabalho Detalhados para Reempacotamento de JIT.](../~old-creative-repackaging-service/jit-repackage.md) Se o servidor de manifesto receber a variável `ptplayer=ios-mobileweb` , instrui o CRS a injetar pacotes de ID3 no anúncio transcodificado antes de carregá-lo no servidor CDN.

>[!NOTE]
>
>Em uma configuração de vários CDNs, o servidor de manifesto usa o `ptcdn` no URL de inicialização para identificar o servidor CDN ao qual carregar o criativo do anúncio.