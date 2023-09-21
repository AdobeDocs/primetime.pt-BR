---
title: Transcodificação e normalização
description: Transcodificação e normalização
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Transcodificação e normalização {#transcoding-and-normalization}

O Primetime Ad Insertion tentará garantir uma experiência de exibição consistente no conteúdo e nos anúncios, tentando corresponder:

1. Codecs de fluxo de origem e taxas de bits, enquanto sempre seleciona a mais alta qualidade/taxa de bits criativo ao transcodificar

1. Tamanhos de fragmento de fluxo de origem (HLS/#EXT-X-TARGETDURATION)

1. Formatos criativos preferidos para transcodificação

1. Nivelamento automático de áudio para garantir um nível de dB consistente em todas as criações de anúncios.

>[!NOTE]
>
>Ad Insertion Os ativos HLS gerados pela transcodificação just-in-time do Primetime produzem ativos HLS da versão 3, independentemente de qual versão do HLS está definida no conteúdo.
