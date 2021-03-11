---
description: Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão de anúncio do Adobe Primetime.
title: Configurar metadados de inserção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão de anúncio do Adobe Primetime.

>[!TIP]
>
>O Adobe Primetime ad decisioning era anteriormente conhecido como Auditude.

Metadados de publicidade estão na propriedade `MediaResource.Metadata` . Ao iniciar a reprodução de um novo vídeo, o aplicativo é responsável por definir os metadados de anúncio corretos.

1. Crie a instância `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina o Adobe Primetime ad decisioning `mediaID`, `zoneID`, `domain` e os parâmetros opcionais de direcionamento.

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
   >A ID de mídia é consumida pelo TVSDK como uma cadeia de caracteres, que é convertida em um valor md5 e é usada para o valor `u` na solicitação de URL de decisão do Primetime. Por exemplo:
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

1. Crie uma instância `MediaResource` usando o URL de fluxo de mídia e os metadados de anúncio criados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Carregue o objeto `MediaResource` pelo método `MediaPlayer.replaceCurrentResource`.

   O `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando o `MediaPlayer` for transferido para o status `INITIALIZED`, obtenha as características do fluxo de mídia no formato de uma instância `MediaPlayerItem` por meio do método `MediaPlayer.CurrentItem`.
1. (Opcional) Consulte a instância `MediaPlayerItem` para ver se o fluxo está ao vivo, independentemente de ter trilhas de áudio alternativas ou se o fluxo está protegido.

   Essas informações podem ajudar você a preparar a interface do usuário para a reprodução. Por exemplo, se você sabe que há duas faixas de áudio, é possível incluir um controle de interface do usuário que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios forem resolvidos e colocados na linha do tempo, o `MediaPlayer` será transferido para o estado `PREPARED`.
1. Chame `MediaPlayer.play` para iniciar a reprodução.

O TVSDK agora inclui anúncios quando a mídia é reproduzida.
