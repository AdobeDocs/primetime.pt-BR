---
description: Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão de anúncio do Adobe Primetime.
title: Configurar metadados de inserção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Configurar metadados de inserção de anúncio{#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings para configurar os metadados de decisão de anúncio do Adobe Primetime.

>[!TIP]
>
>O Adobe Primetime ad decisioning era anteriormente conhecido como Auditude .

1. Crie a instância `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina a ID de mídia de decisão do anúncio do Adobe Primetime, a zoneID, o domínio e os parâmetros de definição de metas opcionais.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Crie uma instância `MediaResource` usando o URL de fluxo de mídia e os metadados de anúncio criados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Carregue o objeto `MediaResource` pelo método `MediaPlayer.replaceCurrentResource(resource)`.

   O `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando o `MediaPlayer` for transferido para o status INITIALIZED , obtenha as características do fluxo de mídia no formato de uma instância `MediaPlayerItem` por meio do atributo `MediaPlayer.CurrentItem`.
1. (Opcional) Consulte a instância `MediaPlayerItem` para ver se o fluxo está ao vivo, independentemente de ter trilhas de áudio alternativas.

   Essas informações podem ajudar você a preparar a interface do usuário para a reprodução. Por exemplo, se você sabe que há duas faixas de áudio, é possível incluir um controle de interface do usuário que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios tiverem sido resolvidos e colocados na linha do tempo, o `  MediaPlayer ` será transferido para o estado PREPARADO.
1. Chame `MediaPlayer.play` para iniciar a reprodução.
O TVSDK do navegador agora inclui anúncios quando a mídia é reproduzida.
