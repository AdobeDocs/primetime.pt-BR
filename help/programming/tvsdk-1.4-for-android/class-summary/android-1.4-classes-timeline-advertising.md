---
description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
seo-description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
seo-title: Classes de anúncios de linha do tempo
title: Classes de anúncios de linha do tempo
uuid: 4e6ca9fb-9e68-4625-a24b-386a50333862
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classes de anúncios de linha do tempo{#timeline-advertising-classes}

Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.

Pacote: [com.adobe.mediacore.timeline.advertit](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Pacote: [com.adobe.mediacore.timeline.publish.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nome | Descrição |
|--- |--- |
| [Anúncio](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe que define a abstração do anúncio e contém todas as informações do anúncio. É definida por uma ID exclusiva, uma duração e uma `MediaResource`. O `MediaResource` contém o URL no qual o conteúdo real do anúncio reside. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe que representa um ativo a ser exibido. Classe que representa um ativo de anúncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe que oferece uma exibição unificada em vários anúncios que serão reproduzidos em algum ponto durante a reprodução. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Classe de operação de colocação de quebra de anúncio. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumeração que define a política de reprodução de anúncio relacionada ao usuário que ignora publicidades durante a busca. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe que representa uma instância de clique associada a um ativo. Esta instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interface que define as propriedades para chamadas da API AdPolicySelector. Essas propriedades fornecem o contexto para impor cada comportamento de anúncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Uma interface do seletor de política de publicidade para impor comportamentos de publicidade. Os aplicativos podem estar em conformidade com essa interface implementando todos os métodos necessários ou estendendo a classe do seletor de política padrão existente para personalizar comportamentos específicos. |
| `auditude.AuditudeAdProvider` | Obsoleto. Use o AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Classe que lida com o anúncio primetime resolvendo no processo de Frase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Classe que implementa a interface do ContentTracker e define eventos de rastreamento de anúncios Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Classe que lida com a peça que resolve o anúncio no processo Frase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interface que define o protocolo que você deve implementar se quiser criar um módulo de rastreamento de anúncios que seja projetado para integração com a biblioteca ou com um rastreador de anúncios personalizado. Essa interface exige que você defina a forma como os eventos de progresso de anúncio são reportados ao sistema remoto de rastreamento de anúncios. |
| [PosicionamentoInformações](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Classe que abstrai uma solicitação de informações de posicionamento. Cada anúncio resolvido deve ter uma informação de posicionamento anexada a ele. As informações de posicionamento descrevem onde o anúncio deve ser colocado na linha do tempo. Ele contém informações como: <ul><li>Posição da disposição (em ms) </li><li>Tipo de posicionamento (pre-roll, mid-roll ou post-roll) </li><li>Duração do bloco de conteúdo principal que está prestes a ser substituído</li></ul> |
