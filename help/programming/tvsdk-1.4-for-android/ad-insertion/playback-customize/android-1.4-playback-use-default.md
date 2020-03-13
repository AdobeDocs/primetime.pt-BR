---
description: Você pode optar por usar comportamentos de publicidade padrão.
seo-description: Você pode optar por usar comportamentos de publicidade padrão.
seo-title: Usar o comportamento de reprodução padrão
title: Usar o comportamento de reprodução padrão
uuid: ccda5223-17c1-4cda-b875-e706f5dc8648
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

Para usar comportamentos padrão:

    * Se você implementar sua própria classe &quot;AdvertisingFactory&quot;, retorne null para &quot;createAdPolicySelector&quot;.
    
    * Se você não tiver uma implementação personalizada para a classe &quot;AdvertisingFactory&quot;, o TVSDK usará um seletor de política de publicidade padrão.