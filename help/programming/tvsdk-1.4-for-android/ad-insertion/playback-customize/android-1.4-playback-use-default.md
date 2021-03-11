---
description: Você pode optar por usar comportamentos de publicidade padrão.
title: Usar o comportamento de reprodução padrão
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

Para usar comportamentos padrão:

    * Se você implementar sua própria classe &quot;AdvertisingFactory&quot;, retorne null para &quot;createAdPolicySelector&quot;.
    
    * Se você não tiver uma implementação personalizada para a classe &quot;AdvertisingFactory&quot;, o TVSDK usa um seletor de política de anúncio padrão.