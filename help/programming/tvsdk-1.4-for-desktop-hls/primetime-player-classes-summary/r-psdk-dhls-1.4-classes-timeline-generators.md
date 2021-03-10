---
description: Essas classes ajudam a detectar oportunidades em uma linha do tempo para posicionar conteúdo, como anúncios.
title: Classes de geradores de linha do tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Classes de geradores de linha do tempo{#timeline-generators-classes}

Essas classes ajudam a detectar oportunidades em uma linha do tempo para posicionar conteúdo, como anúncios.

Pacote: [com.adobe.mediacore.timeline.geradores](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nome | Descrição |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Classe que cria uma oportunidade inicial para o modo de sinalização de publicidade especificado. |
| [OportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Classe de base para todos os geradores de oportunidade. |
| [OportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interface usada por geradores de oportunidade para se comunicar com componentes TVSDK. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Classe que monitora a linha do tempo de reprodução e detecta oportunidades de posicionamento de anúncio inseridas no manifesto como comentários SpliceOut. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementação padrão de um gerador de oportunidades que está usando informações de metadados cronometrados para detectar e gerar oportunidades de anúncio. |