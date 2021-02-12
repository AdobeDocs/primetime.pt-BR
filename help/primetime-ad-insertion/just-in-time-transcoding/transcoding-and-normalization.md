---
title: Transcodificação e normalização
description: null
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Transcodificação e normalização {#transcoding-and-normalization}

O Primetime Ad Insertion tentará garantir uma experiência de visualização consistente em todo o conteúdo e anúncios, tentando corresponder:

1. Codecs de fluxo de origem e taxas de bits, ao mesmo tempo em que seleciona a mais alta qualidade/taxa de bits criativa ao transcodificar

1. Tamanhos de fragmento do fluxo de origem (HLS/#EXT-X-TARGETDURATION)

1. Formatos criativos preferidos para transcodificação

1. Nivelamento automático de áudio para garantir um nível dB consistente em todos os anúncios.

>[!NOTE]
>
>Os ativos HLS gerados pela transcodificação de tempo just-in do Ad Insertion Primetime produzem ativos HLS da versão 3, independentemente da versão HLS definida no conteúdo.