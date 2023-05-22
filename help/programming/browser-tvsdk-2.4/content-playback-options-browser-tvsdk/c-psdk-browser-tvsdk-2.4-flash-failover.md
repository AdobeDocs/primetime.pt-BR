---
description: O TVSDK do navegador fornece ferramentas para criar um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime.
title: Failover do Flash
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Failover do Flash {#flash-failover}

O TVSDK do navegador fornece ferramentas para criar um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime.

Use as ferramentas da sua plataforma para criar um reprodutor e conectá-lo à visualização do reprodutor de mídia no TVSDK do navegador, que tem métodos para reproduzir e gerenciar vídeos. Por exemplo, o TVSDK do navegador fornece métodos de reprodução e pausa. Você pode criar botões de interface do usuário na plataforma e definir os botões para chamar os métodos TVSDK do navegador.

## Fallback de Flash {#section_92D3884A13A6431F9A9CC5C79715D888}

No TVSDK do navegador, seu aplicativo interage somente com o `Primetime.js` API. A implementação TVSDK do navegador subjacente decide qual tecnologia de player usar com base na plataforma atual e no tipo de recurso da mídia a ser reproduzida.

A decisão para a tecnologia do reprodutor não é tomada até que você chame `MediaPlayer.replaceCurrentResource` para reproduzir um recurso específico.

Por exemplo:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determine o reprodutor de mídia a ser usado {#section_D844E386AF5848688D204DEE258ECEE6}

Este procedimento de amostra ilustra o processo de determinação da tecnologia do reprodutor:

>[!TIP]
>
>O processo pode variar dependendo do URL e do seu ambiente.

1. Se as extensões de origem de mídia forem compatíveis, use-as sem limitações conhecidas.
1. Se suportado, use o `<video>` tag diretamente sem o MSE.
1. Verifique se você está usando pelo menos a versão 23.0 do Flash Player do Adobe.
1. Se nenhuma tecnologia de reprodução adequada for encontrada, `replaceCurrentResource` retorna um erro.

Um subsequente `replaceCurrentResource` chamar na mesma `MediaPlayer` instância segue o mesmo processo. Isso permite reproduzir vários tipos de recursos usando o mesmo `MediaPlayer` instância no mesmo pai `<DIV>` que você especificou quando a variável `MediaPlayerView` instância foi criada.

>[!TIP]
>
>O objeto SWF e a variável `<video>` são aninhadas no pai `<DIV>` tag.
