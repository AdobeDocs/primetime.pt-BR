---
description: Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão de anúncio do Adobe Primetime.
seo-description: Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão de anúncio do Adobe Primetime.
seo-title: Configurar metadados de inserção de anúncio
title: Configurar metadados de inserção de anúncio
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Configurar metadados de inserção de anúncio{#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão de anúncio do Adobe Primetime.

>[!TIP]
>
>A decisão do anúncio do Adobe Primetime era anteriormente conhecida como Auditude.

1. Crie a instância `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina a ID de mídia de decisão de publicidade da Adobe Primetime, zoneID, domínio e os parâmetros de definição de metas opcionais.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Crie uma instância `MediaResource` usando o URL de fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Carregue o objeto `MediaResource` pelo método `MediaPlayer.replaceCurrentResource(resource)`.

   O `MediaPlayer` start o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando `MediaPlayer` transição para o status INITIALIZED, obtenha as características de fluxo de mídia na forma de uma instância `MediaPlayerItem` por meio do atributo `MediaPlayer.CurrentItem`.
1. (Opcional) Query a instância `MediaPlayerItem` para ver se o fluxo está ao vivo, independentemente de ter faixas de áudio alternativas.

   Estas informações podem ajudá-lo a preparar a interface para a reprodução. Por exemplo, se você sabe que existem duas faixas de áudio, é possível incluir um controle de interface que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para start do fluxo de trabalho de publicidade.

   Depois que as publicidades forem resolvidas e colocadas na linha do tempo, a `  MediaPlayer ` transição para o estado PREPARADO.
1. Chame `MediaPlayer.play` para start da reprodução.
O TVSDK do navegador agora inclui anúncios quando sua mídia é reproduzida.
