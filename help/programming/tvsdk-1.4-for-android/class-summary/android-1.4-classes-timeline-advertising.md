---
description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
title: Classes de publicidade da linha do tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# Classes de publicidade da linha do tempo{#timeline-advertising-classes}

Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.

Pacote: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Pacote: [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nome | Descrição |
|--- |--- |
| [Publicidade](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe que define a abstração do anúncio e mantém todas as informações do anúncio. É definido por uma ID exclusiva, uma duração e um `MediaResource`. O `MediaResource` contém o URL onde reside o conteúdo real do anúncio. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe que representa um ativo a ser exibido. Classe que representa um ativo de anúncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe que fornece uma exibição unificada em vários anúncios que serão reproduzidos em algum ponto durante a reprodução. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Classe de operação de inserção de quebra de anúncio. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumeração que define a política de reprodução de anúncio relacionada ao usuário ignorando anúncios durante a busca. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe que representa uma instância de clique associada a um ativo. Essa instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interface que define as propriedades para chamadas da API AdPolicySelector . Essas propriedades fornecem o contexto para impor cada comportamento de anúncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Uma interface do seletor de política de publicidade para aplicar comportamentos de publicidade. Os aplicativos podem estar em conformidade com essa interface implementando todos os métodos necessários ou estendendo a classe do seletor de políticas padrão existente para personalizar comportamentos específicos. |
| `auditude.AuditudeAdProvider` | Obsoleto. Use AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Classe que lida com o primetime e é resolvida no processo Frase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Classe que implementa a interface do ContentTracker e define eventos de rastreamento de anúncios do Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Classe que trata a parte que resolve o anúncio no processo Frase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interface que define o protocolo que deve ser implementado se você quiser criar um módulo de rastreamento de anúncios criado para integrar com a biblioteca ou um rastreador de anúncios personalizado. Essa interface exige que você defina a forma como os eventos de progresso do anúncio são relatados no sistema remoto de rastreamento de anúncios. |
| [InserçãoInformações](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Classe que abstrai uma solicitação de informações de posicionamento. Cada anúncio resolvido deve ter uma informação de posicionamento anexada a ele. As informações de posicionamento descrevem onde o anúncio deve ser colocado na linha do tempo. Ele contém informações como: <ul><li>Posição da disposição (em ms) </li><li>Tipo de disposição (precedente, intermediário ou posterior) </li><li>Duração do bloco de conteúdo principal que está prestes a ser substituído</li></ul> |
