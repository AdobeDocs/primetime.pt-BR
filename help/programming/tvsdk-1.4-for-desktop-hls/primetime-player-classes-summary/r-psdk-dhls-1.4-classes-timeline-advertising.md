---
description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
title: Classes de publicidade da linha do tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Classes de publicidade da linha do tempo {#timeline-advertising-classes}

Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.

Pacote: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Pacote: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nome | Descrição |
|---|---|
| [Publicidade](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe que define a abstração do anúncio e mantém todas as informações do anúncio. É definido por uma ID exclusiva, uma duração e um `MediaResource`. O `MediaResource` contém o URL onde reside o conteúdo real do anúncio. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe que representa um ativo a ser exibido. Classe que representa um ativo de anúncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe que fornece uma exibição unificada em vários anúncios que serão reproduzidos em algum ponto durante a reprodução. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumeração que define a política de reprodução de anúncio relacionada ao usuário ignorando anúncios durante a busca. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Item de linha do tempo associado ao ad break específico. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Classe de enumeração para possíveis políticas sobre quando marcar um ad break como tendo sido observado. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe que representa uma instância de clique associada a um ativo. Essa instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Classe de enumeração para possíveis políticas sobre onde retomar a reprodução de um ad break após o modo de busca ou reprodução de artifício. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Classe de enumeração que lista as maneiras em que o reprodutor está sendo reproduzido, como busca ou reprodução normal. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interface que define as propriedades para chamadas da API `AdPolicySelector`. Essas propriedades fornecem o contexto para impor cada comportamento de anúncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Uma interface do seletor de política de publicidade para aplicar comportamentos de publicidade. Os aplicativos podem estar em conformidade com essa interface implementando todos os métodos necessários ou estendendo a classe do seletor de políticas padrão existente para personalizar comportamentos específicos. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Item de linha do tempo associado a um anúncio específico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Classe que lida com o primetime e é resolvida no processo TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumeração de todos os tipos de anúncios compatíveis com o TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Classe. |

