---
description: Essas classes ajudam a detectar oportunidades em uma linha do tempo para posicionar conteúdo, como anúncios.
seo-description: Essas classes ajudam a detectar oportunidades em uma linha do tempo para posicionar conteúdo, como anúncios.
seo-title: Classes de geradores de linha do tempo
title: Classes de geradores de linha do tempo
uuid: 1e36b738-0684-44f0-b3c3-dd656c70f705
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Classes de geradores de linha do tempo{#timeline-generators-classes}

Essas classes ajudam a detectar oportunidades em uma linha do tempo para posicionar conteúdo, como anúncios.

Pacote: [com.adobe.mediacore.timeline.geradores](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Nome | Descrição |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | Classe que cria uma oportunidade inicial para o modo de sinalização de publicidade especificado. |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Classe base para todos os geradores de oportunidade. |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Interface usada pelos geradores de oportunidade para se comunicar com componentes TVSDK. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | Classe que monitora a linha do tempo de reprodução e detecta oportunidades de posicionamento de anúncio inseridas no manifesto como comentários SpliceOut. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Implementação padrão de um gerador de oportunidades que está usando informações de metadados cronometrados para detectar e gerar oportunidades de anúncio. |