---
description: Um detector de oportunidade é um componente TVSDK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
title: Geradores de oportunidades e resolvedores de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Geradores de oportunidades e resolvedores de conteúdo {#opportunity-generators-and-content-resolvers}

Um detector de oportunidade é um componente TVSDK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK inclui um detector de oportunidade padrão:

* `SpliceOutPlacementOpportunityDetector`, que entende as dicas de anúncio padrão

O TVSDK também inclui resolvedores de conteúdo padrão que fornecem conteúdo a ser inserido com base na chave de metadados no item do player:

* `AuditudeResolver` para  `AUDITUDE_METADATA_KEY`, que é capaz de se comunicar com os servidores de decisão de anúncios da Adobe Primetime (anteriormente conhecidos como Auditude) e de retornar as quebras de anúncios para colocar.

* `MetadataResolver` para  `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` para  `TIME_RANGES_METADATA_KEY`

Você pode substituir os detectores de oportunidade e os resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção personalizada de tags
* Reconhecer tags personalizadas para inserção de anúncios
* Criar um provedor de publicidade personalizado
* Conteúdo preto

O TVSDK fornece geradores de oportunidades padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de posicionamento de anúncios. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo, como um período de blecaute. Um *`opportunity generator`* identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK de que essas oportunidades foram marcadas. As oportunidades são identificadas em uma linha do tempo no ao incluir uma tag não padrão (não HLS).

Quando seu aplicativo é notificado sobre uma oportunidade (tag), seu aplicativo pode alterar a linha do tempo, por exemplo, inserindo uma série de anúncios, alternando para um fluxo alternativo (blecautes) ou editando o conteúdo da linha do tempo. Por padrão, o TVSDK chama o *`content resolver`* apropriado para implementar as alterações ou ações necessárias da linha do tempo. Seu aplicativo pode usar o resolvedor de conteúdo de anúncio TVSDK padrão ou registrar seu próprio resolvedor de conteúdo.

Você também pode usar `MediaPlayerItemConfig.setAdTags` para adicionar mais marcadores de anúncio/dicas, de modo que o TVSDK possa reconhecer e usar `MediaPlayerItemConfig.subscribedTags` e notificar seu aplicativo sobre marcadores adicionais que possam ter informações de fluxo de trabalho de publicidade.

Um possível uso de um resolvedor personalizado é para períodos de blecaute. Para lidar com esses períodos, seu aplicativo pode implementar e registrar um detector de oportunidade de blecaute responsável por manipular tags de blecaute. Quando o TVSDK encontra essa tag, ele pesquisa todos os resolvedores de conteúdo registrados para localizar o primeiro que manipula a tag especificada. Neste exemplo, é o resolvedor de conteúdo do blackout, que pode, por exemplo, substituir o item atual por conteúdo alternativo no reprodutor pela duração especificada pela tag .
