---
description: Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão de anúncio do Adobe Primetime.
seo-description: Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão de anúncio do Adobe Primetime.
seo-title: Configurar metadados de inserção de anúncio
title: Configurar metadados de inserção de anúncio
uuid: 5c807fad-4927-4547-b58c-f37e505e651c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão de anúncio do Adobe Primetime.

>[!TIP]
>
>A decisão do anúncio da Adobe Primetime era anteriormente conhecida como Auditude.

Os metadados de publicidade estão na propriedade `MediaResource.Metadata`. Ao iniciar a reprodução de um novo vídeo, seu aplicativo é responsável por definir os metadados de publicidade corretos.

1. Crie a instância `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Defina as decisões de publicidade do Adobe Primetime `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>` e os parâmetros de definição de metas opcionais.

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
   >A ID de mídia é consumida pelo TVSDK como uma string, que é convertida em um valor md5 e é usada para o valor `u` na solicitação de URL de decisão do Primetime ad. Por exemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crie uma instância `MediaResource` usando o URL de fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Carregue o objeto `MediaResource` pelo método `MediaPlayer.replaceCurrentResource`.

   O `MediaPlayer` start o carregamento e o processamento do manifesto de fluxo de mídia.

1. Quando `MediaPlayer` transição para o status INITIALIZED, obtenha as características de fluxo de mídia na forma de uma instância `MediaPlayerItem` pelo método `MediaPlayer.CurrentItem`.
1. (Opcional) Query a instância `MediaPlayerItem` para ver se o fluxo está ao vivo, independentemente de ter faixas de áudio alternativas ou se o fluxo está protegido.

   Estas informações podem ajudá-lo a preparar a interface para a reprodução. Por exemplo, se você sabe que existem duas faixas de áudio, é possível incluir um controle de interface que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para start do fluxo de trabalho de publicidade.

   Depois que as publicidades forem resolvidas e colocadas na linha do tempo, a `MediaPlayer` transição para o estado `PREPARED`.
1. Chame `MediaPlayer.play` para start da reprodução.

O TVSDK agora inclui anúncios quando sua mídia é reproduzida.