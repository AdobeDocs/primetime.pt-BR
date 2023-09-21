---
description: Use a classe auxiliar AuditudeSettings para configurar os metadados do Adobe Primetime ad decisioning.
title: Configurar metadados de inserção de anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Configurar metadados de inserção de anúncio{#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings para configurar os metadados do Adobe Primetime ad decisioning.

>[!TIP]
>
>O Adobe Primetime Ad Decisioning era anteriormente conhecido como Auditude .

1. Crie o `AuditudeSettings` instância.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina a mediaID, a zoneID, o domínio e os parâmetros opcionais de direcionamento do Adobe Primetime ad decisioning.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Criar um `MediaResource` usando o URL do fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Carregue o `MediaResource` por meio do `MediaPlayer.replaceCurrentResource(resource)` método.

   A variável `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando a variável `MediaPlayer` para o status INITIALIZED, obtenha as características do fluxo de mídia na forma de um `MediaPlayerItem` por meio da `MediaPlayer.CurrentItem` atributo.
1. (Opcional) Consulte as `MediaPlayerItem` instância para ver se o fluxo está ativo, independentemente de ter faixas de áudio alternativas.

   Essas informações podem ajudar você a preparar a interface do usuário para a reprodução. Por exemplo, se você souber que existem duas faixas de áudio, poderá incluir um controle de interface do usuário que alterna entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios forem resolvidos e colocados na linha do tempo, a variável `  MediaPlayer ` transições para o estado PREPARADO.
1. Chame `MediaPlayer.play` para iniciar a reprodução.
O TVSDK do navegador agora inclui anúncios quando a mídia é reproduzida.
