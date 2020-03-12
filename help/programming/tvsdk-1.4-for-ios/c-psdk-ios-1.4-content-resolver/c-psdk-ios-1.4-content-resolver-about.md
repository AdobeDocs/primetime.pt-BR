---
description: O TVSDK fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.
seo-description: O TVSDK fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.
seo-title: Geradores de oportunidade e resolvedores de conteúdo
title: Geradores de oportunidade e resolvedores de conteúdo
uuid: e1d658eb-cb6c-407d-9163-2dbf62ba1d19
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Geradores de oportunidade e resolvedores de conteúdo{#opportunity-generators-and-content-resolvers}

Um detector de oportunidade é um componente TVSDK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK inclui um detector de oportunidade padrão:

* `PTOpportunityResolver`, que entende dicas de anúncios padrão

O TVSDK também inclui um resolvedor de conteúdo padrão que fornece conteúdo a ser inserido com base na chave de metadados no item do player:

* `PTContentResolver`

Você pode substituir os detectores de oportunidade padrão e os resolvedores de conteúdo para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção de tags personalizadas
* Reconhecer tags personalizadas para inserção de anúncios
* Criar um provedor de publicidade personalizado
* Conteúdo de saída preta

O TVSDK fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de colocação de anúncio. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo, como um período de blecaute. Um *`opportunity generator`* identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK de que essas oportunidades foram marcadas. As oportunidades são identificadas em uma linha do tempo ao incluir `PTTimedMetadata` uma tag não padrão (não HLS).

Quando seu aplicativo é notificado sobre uma oportunidade (tag), seu aplicativo pode alterar a linha do tempo inserindo, por exemplo, uma série de anúncios, alternando para um fluxo alternativo (blecautes) ou editando o conteúdo da linha do tempo. Por padrão, o TVSDK chama o apropriado *`content resolver`* para implementar as alterações ou ações necessárias na linha do tempo. Seu aplicativo pode usar o resolvedor de conteúdo de anúncio TVSDK padrão ou registrar seu próprio resolvedor de conteúdo.

Você também pode usar `PTSDKConfig.setAdTags` para adicionar mais tags/dicas de marcadores de anúncios, de modo que o TVSDK possa reconhecer e usar `PTSDKConfig.setSubscribedTags` e notificar seu aplicativo sobre tags adicionais que possam conter informações de fluxo de trabalho de publicidade.

Um possível uso de um resolvedor personalizado é para períodos de blecaute. Para lidar com esses períodos, seu aplicativo poderia implementar e registrar um detector de oportunidade de blecaute responsável pelo gerenciamento de tags de blecaute. Quando o TVSDK encontra essa tag, ele chama todos os resolvedores de conteúdo registrados para localizar o primeiro que manipula a tag especificada. Neste exemplo, é o resolvedor de conteúdo de blecaute, que pode, por exemplo, substituir o item atual por conteúdo alternativo no player pela duração especificada pela tag .
