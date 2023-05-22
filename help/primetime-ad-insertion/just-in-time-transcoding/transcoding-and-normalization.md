---
title: Transcodificação e normalização
description: Transcodificação e normalização
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Transcodificação e normalização {#transcoding-and-normalization}

O Ad Insertion do Primetime tentará garantir uma experiência de exibição consistente no conteúdo e nos anúncios, tentando corresponder:

1. Codecs de fluxo de origem e taxas de bits, enquanto sempre seleciona a mais alta qualidade/taxa de bits criativo ao transcodificar

1. Tamanhos de fragmento de fluxo de origem (HLS/#EXT-X-TARGETDURATION)

1. Formatos criativos preferidos para transcodificação

1. Nivelamento automático de áudio para garantir um nível de dB consistente em todas as criações de anúncios.

>[!NOTE]
>
>Ad Insertion Os ativos HLS gerados pela transcodificação just-in-time do Primetime produzem ativos HLS da versão 3, independentemente de qual versão do HLS está definida no conteúdo.
