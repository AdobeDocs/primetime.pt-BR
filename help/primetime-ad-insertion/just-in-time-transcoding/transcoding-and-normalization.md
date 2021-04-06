---
title: Transcodificação e normalização
description: Transcodificação e normalização
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Transcodificação e normalização {#transcoding-and-normalization}

O Primetime Ad Insertion tentará garantir uma experiência de visualização consistente entre o conteúdo e os anúncios ao tentar corresponder a:

1. Codecs de fluxo de origem e taxas de bits, ao mesmo tempo em que seleciona a criação de maior qualidade/taxa de bits ao transcodificar

1. Tamanhos de fragmento de fluxo de origem (HLS/#EXT-X-TARGETDURATION)

1. Formatos criativos preferidos para transcodificação

1. Nivelamento automático de áudio para garantir um nível dB consistente em todas as criações de anúncios.

>[!NOTE]
>
>Os ativos HLS gerados pela transcodificação de tempo just-in do Ad Insertion do Primetime produzem ativos HLS da versão 3, independentemente da versão HLS definida no conteúdo.
