---
description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
title: Classes de publicidade da linha do tempo
exl-id: 2ac1f6b7-48b2-4d9c-b39d-a7e6f1ff2ac5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
| [Anúncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe que define a abstração do anúncio e contém todas as informações do anúncio. É definida por um identificador exclusivo, uma duração e uma `MediaResource`. A variável `MediaResource` contém o URL onde o conteúdo real do anúncio está. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe que representa um ativo a ser exibido. Classe que representa um ativo de anúncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe que fornece uma visualização unificada de vários anúncios que serão reproduzidos em algum momento durante a reprodução. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumeração que define a política de reprodução de anúncio relacionada ao usuário que ignora anúncios durante a busca. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Item de linha do tempo associado ao ad break específico. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Classe de enumeração para possíveis políticas sobre quando marcar um ad break como observado. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe que representa uma instância de clique associada a um ativo. Essa instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Classe de enumeração para possíveis políticas sobre onde retomar a reprodução de um ad break após o modo de busca ou de truque. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Classe de enumeração que lista as maneiras pelas quais o player está reproduzindo, como busca ou reprodução normal. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interface que define propriedades para `AdPolicySelector` Chamadas de API. Essas propriedades fornecem o contexto para impor cada comportamento de anúncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Uma interface de seletor de políticas de anúncios para impor comportamentos de anúncios. Os aplicativos podem estar em conformidade com essa interface implementando todos os métodos necessários ou estendendo a classe padrão do seletor de políticas existente para personalizar comportamentos específicos. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Item da linha do tempo associado a um anúncio específico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Classe que lida com o primetime e a resolução no processo TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumeração de todos os tipos de anúncios aos quais o TVSDK oferece suporte. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Classe. |
