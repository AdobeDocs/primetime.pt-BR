---
description: O TVSDK do navegador fornece ferramentas para criar um aplicativo avançado de player de vídeo (seu player do Primetime), que pode ser integrado a outros componentes do Primetime.
title: Failover de Flash
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Failover de Flash {#flash-failover}

O TVSDK do navegador fornece ferramentas para criar um aplicativo avançado de player de vídeo (seu player do Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da plataforma para criar um reprodutor e conectá-lo à exibição do reprodutor de mídia no Browser TVSDK, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK do navegador fornece métodos de reprodução e pausa. Você pode criar botões da interface do usuário na sua plataforma e definir os botões para chamar esses métodos TVSDK do navegador.

## Flash de fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

No TVSDK do navegador, seu aplicativo interage somente com a API `Primetime.js`. A implementação subjacente do TVSDK do Navegador decide qual tecnologia do player usar com base na plataforma atual e no tipo de recurso da mídia a ser reproduzida.

A decisão da tecnologia do player não é tomada até que você chame `MediaPlayer.replaceCurrentResource` para reproduzir um recurso específico.

Por exemplo:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determine o reprodutor de mídia a ser usado {#section_D844E386AF5848688D204DEE258ECEE6}

Este procedimento de amostra ilustra o processo de determinação da tecnologia do player:

>[!TIP]
>
>O processo pode variar dependendo do URL e do seu ambiente.

1. Se as extensões de origem da mídia forem compatíveis, use-as sem limitações conhecidas.
1. Se suportado, use a tag `<video>` diretamente sem MSE.
1. Verifique se você está usando pelo menos o Adobe Flash Player versão 23.0.
1. Se nenhuma tecnologia de reprodução adequada for encontrada, `replaceCurrentResource` retornará um erro.

Uma chamada `replaceCurrentResource` subsequente na mesma instância `MediaPlayer` segue o mesmo processo. Isso permite reproduzir vários tipos de recursos usando a mesma instância `MediaPlayer` na mesma tag principal `<DIV>` que você especificou quando a instância `MediaPlayerView` foi criada.

>[!TIP]
>
>O Objeto SWF e a tag `<video>` são aninhados na tag principal `<DIV>`.

