---
description: Você pode optar por usar comportamentos de anúncio padrão.
title: Usar o comportamento de reprodução padrão
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de anúncio padrão.

Para usar comportamentos padrão:

    * Se você implementar sua própria classe &quot;AdvertisingFactory&quot;, retorne nulo para &quot;createAdPolicySelector&quot;.
    
    * Se você não tiver uma implementação personalizada para a classe &quot;AdvertisingFactory&quot;, o TVSDK usará um seletor de política de anúncio padrão.
