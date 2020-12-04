---
description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
seo-description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
seo-title: Classes de anúncios de linha do tempo
title: Classes de anúncios de linha do tempo
uuid: f424fa13-778b-458d-bc82-389441a8a56a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Classes de anúncios de linha do tempo {#timeline-advertising-classes}

Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.

Pacote: [com.adobe.mediacore.timeline.publish](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Pacote: [com.adobe.mediacore.timeline.publish.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nome | Descrição |
|---|---|
| [Anúncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe que define a abstração do anúncio e contém todas as informações do anúncio. É definida por uma ID exclusiva, uma duração e um `MediaResource`. O `MediaResource` contém o URL no qual o conteúdo real do anúncio reside. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe que representa um ativo a ser exibido. Classe que representa um ativo de anúncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe que fornece uma visualização unificada em vários anúncios que serão reproduzidos em algum ponto durante a reprodução. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Lista discriminada que define a política de reprodução de anúncio relacionada ao usuário que ignora publicidades ao buscar. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Item de linha do tempo associado ao intervalo de anúncios específico. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | classe lista discriminada para possíveis políticas sobre quando marcar uma pausa de anúncio como tendo sido observada. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe que representa uma instância de clique associada a um ativo. Esta instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | classe lista discriminada para possíveis políticas sobre onde retomar a reprodução de um intervalo de anúncio após o modo de busca ou reprodução de truques. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Classe de lista discriminada que lista maneiras em que o player está sendo reproduzido, como busca ou reprodução normal. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interface que define as propriedades para chamadas `AdPolicySelector` da API. Essas propriedades fornecem o contexto para impor cada comportamento de anúncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Uma interface do seletor de política de publicidade para impor comportamentos de publicidade. Os aplicativos podem estar em conformidade com essa interface implementando todos os métodos necessários ou estendendo a classe do seletor de política padrão existente para personalizar comportamentos específicos. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Item de linha do tempo associado a um anúncio específico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Classe que lida com a resolução de anúncios do Primetime no processo do TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Lista discriminada de todos os tipos de anúncios suportados pelo TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Classe. |

