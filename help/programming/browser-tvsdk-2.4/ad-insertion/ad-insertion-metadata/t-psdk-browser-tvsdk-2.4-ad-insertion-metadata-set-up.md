---
description: Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão do anúncio do Adobe Primetime.
seo-description: Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão do anúncio do Adobe Primetime.
seo-title: Configurar metadados de inserção de anúncio
title: Configurar metadados de inserção de anúncio
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Configurar metadados de inserção de anúncio{#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão do anúncio do Adobe Primetime.

>[!TIP]
>
>A decisão do anúncio do Adobe Primetime era anteriormente conhecida como Auditude.

1. Crie a `AuditudeSettings` instância.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina a ID da mídia de decisão do anúncio do Adobe Primetime, a ID da zona, o domínio e os parâmetros de definição de metas opcionais.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Crie uma `MediaResource` instância usando o URL de fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Carregue o `MediaResource` objeto pelo `MediaPlayer.replaceCurrentResource(resource)` método.

   O `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando as transições forem `MediaPlayer` para o status INICIALIZADO, obtenha as características de fluxo de mídia na forma de uma `MediaPlayerItem` instância pelo `MediaPlayer.CurrentItem` atributo.
1. (Opcional) Consulte a `MediaPlayerItem` instância para ver se o fluxo é ao vivo, independentemente de ele ter faixas de áudio alternativas.

   Estas informações podem ajudá-lo a preparar a interface para a reprodução. Por exemplo, se você sabe que existem duas faixas de áudio, é possível incluir um controle de interface que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios forem resolvidos e colocados na linha do tempo, eles serão `  MediaPlayer ` transferidos para o estado PREPARADO.
1. Chame `MediaPlayer.play` para iniciar a reprodução.
O TVSDK do navegador agora inclui anúncios quando sua mídia é reproduzida.
