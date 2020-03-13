---
description: Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão do anúncio do Adobe Primetime.
seo-description: Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão do anúncio do Adobe Primetime.
seo-title: Configurar metadados de inserção de anúncio
title: Configurar metadados de inserção de anúncio
uuid: d96e67c3-4cc7-4309-a2a2-ff5193b46534
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão do anúncio do Adobe Primetime.

>[!TIP]
>
>A decisão do anúncio do Adobe Primetime era anteriormente conhecida como Auditude.

Os metadados de publicidade estão na `MediaResource.Metadata` propriedade. Ao iniciar a reprodução de um novo vídeo, seu aplicativo é responsável por definir os metadados de publicidade corretos.

1. Crie a `AuditudeSettings` instância.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina a decisão do anúncio do Adobe Primetime `mediaID`, `zoneID`e `domain`os parâmetros de definição de metas opcionais.

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
   >A ID de mídia é consumida pelo TVSDK como uma string, que é convertida em um valor md5 e é usada para o `u` valor na solicitação de URL de decisão do Primetime ad. Por exemplo:
   >
   >
   ```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. Crie uma `MediaResource` instância usando o URL de fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Carregue o `MediaResource` objeto pelo `MediaPlayer.replaceCurrentResource` método.

   O `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando a transição `MediaPlayer` for para o `INITIALIZED` status, obtenha as características do fluxo de mídia na forma de uma `MediaPlayerItem` instância pelo `MediaPlayer.CurrentItem` método.
1. (Opcional) Consulte a `MediaPlayerItem` instância para ver se o fluxo é ao vivo, independentemente de ter faixas de áudio alternativas ou se o fluxo é protegido.

   Estas informações podem ajudá-lo a preparar a interface para a reprodução. Por exemplo, se você sabe que existem duas faixas de áudio, é possível incluir um controle de interface que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios forem resolvidos e colocados na linha do tempo, eles serão `MediaPlayer` transferidos para o `PREPARED` estado.
1. Chame `MediaPlayer.play` para iniciar a reprodução.

O TVSDK agora inclui anúncios quando sua mídia é reproduzida.
