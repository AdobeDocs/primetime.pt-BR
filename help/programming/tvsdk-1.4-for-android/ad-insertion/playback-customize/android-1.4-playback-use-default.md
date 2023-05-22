---
description: Você pode optar por usar comportamentos de anúncio padrão.
title: Usar o comportamento de reprodução padrão
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de anúncio padrão.

Para usar comportamentos padrão:

    * Se você implementar sua própria classe &quot;AdvertisingFactory&quot;, retorne nulo para &quot;createAdPolicySelector&quot;.
    
    * Se você não tiver uma implementação personalizada para a classe &quot;AdvertisingFactory&quot;, o TVSDK usará um seletor de política de anúncio padrão.
