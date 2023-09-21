---
description: Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar metadados de Adobe Primetime ad decisioning.
title: Configurar metadados de inserção de anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar metadados de Adobe Primetime ad decisioning.

>[!TIP]
>
>O Adobe Primetime ad decisioning era conhecido anteriormente como Auditude.

Os metadados de publicidade estão na `MediaResource.Metadata` propriedade. Ao iniciar a reprodução de um novo vídeo, seu aplicativo é responsável por definir os metadados de publicidade corretos.

1. Crie o `AuditudeSettings` instância.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Definir o Adobe Primetime ad decisioning `mediaID`, `zoneID`, `domain`e os parâmetros opcionais de direcionamento.

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >A ID de mídia é consumida pelo TVSDK como uma string, que é convertida em um valor md5, e é usada para a variável `u` valor na solicitação de URL do Primetime e da decisão. Por exemplo:
   >
   >```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. Criar um `MediaResource` usando o URL do fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Carregue o `MediaResource` por meio do `MediaPlayer.replaceCurrentResource` método.

   A variável `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando a variável `MediaPlayer` transições para o `INITIALIZED` status, obtenha as características do fluxo de mídia no formato de um `MediaPlayerItem` por meio da `MediaPlayer.CurrentItem` método.
1. (Opcional) Consulte as `MediaPlayerItem` instância para ver se o fluxo está ativo, independentemente de ter faixas de áudio alternativas ou se o fluxo está protegido.

   Essas informações podem ajudar você a preparar a interface do usuário para a reprodução. Por exemplo, se você souber que existem duas faixas de áudio, poderá incluir um controle de interface do usuário que alterna entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios forem resolvidos e colocados na linha do tempo, a variável `MediaPlayer` transições para o `PREPARED` estado.
1. Chame `MediaPlayer.play` para iniciar a reprodução.

O TVSDK agora inclui anúncios quando a mídia é reproduzida.
