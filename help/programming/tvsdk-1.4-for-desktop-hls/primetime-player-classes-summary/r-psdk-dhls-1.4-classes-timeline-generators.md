---
description: Essas classes ajudam a detectar oportunidades em uma linha do tempo para colocação de conteúdo, como anúncios.
title: Classes de geradores de linha do tempo
exl-id: 2c9d1f10-fdf6-48b9-8bda-cee291befeab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Classes de geradores de linha do tempo{#timeline-generators-classes}

Essas classes ajudam a detectar oportunidades em uma linha do tempo para colocação de conteúdo, como anúncios.

Pacote: [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nome | Descrição |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Classe que cria uma oportunidade inicial para o modo de sinalização de publicidade especificado. |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Classe base para todos os geradores de oportunidades. |
| [ClienteGeradorOportunidade](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interface usada pelos geradores de oportunidade para se comunicar com componentes TVSDK. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Classe que monitora a linha do tempo de reprodução e detecta oportunidades de posicionamento de anúncios inseridas no manifesto como comentários SpliceOut. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementação padrão de um gerador de oportunidades que está usando informações de metadados cronometrados para detectar e gerar oportunidades de anúncio. |
