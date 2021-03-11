---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.
title: Metadados de inserção do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Metadados de inserção de anúncio {#ad-insertion-metadata}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.

O TVSDK inclui a biblioteca de decisão do anúncio do Primetime. Para que seu conteúdo inclua publicidade do servidor de decisão do Primetime ad, seu aplicativo deve fornecer as seguintes informações necessárias `AuditudeSettings`:

* `mediaID`, que é um identificador exclusivo para a reprodução do vídeo.

   O editor atribui a mediaID ao enviar o conteúdo de vídeo e as informações do anúncio para o servidor de decisão do anúncio do Adobe Primetime. Essa ID é usada pelo Primetime ad Decisioning para recuperar informações de publicidade relacionadas ao vídeo do servidor.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

   Você pode incluir esses parâmetros dependendo das suas necessidades e das necessidades do provedor de anúncios.

## Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings , que estende a classe MetadataNode , para configurar os metadados de decisão de anúncio do Adobe Primetime.

>[!TIP]
>
>O Adobe Primetime ad decisioning era anteriormente conhecido como Auditude.

Metadados de publicidade estão na propriedade `MediaResource.metadata` . Ao iniciar a reprodução de um novo vídeo, o aplicativo é responsável por definir os metadados de anúncio corretos.

1. Crie a instância `AuditudeSettings`.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Defina a ID de mídia de decisão do anúncio do Adobe Primetime, a zoneID, o domínio e os parâmetros de definição de metas opcionais.

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >A ID de mídia é consumida pelo TVSDK como uma cadeia de caracteres, que é convertida em um valor md5 e é usada para o valor `u` na solicitação de URL de decisão do Primetime. Por exemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crie uma instância `MediaResource` usando o URL de fluxo de mídia e os metadados de anúncio criados anteriormente.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Carregue o objeto `MediaResource` pelo método `MediaPlayer.replaceCurrentResource`.

   O `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. (Opcional) Consulte a instância `MediaPlayerItem` para ver se o fluxo está ao vivo, independentemente de ter trilhas de áudio alternativas ou se o fluxo está protegido.

   Essas informações podem ajudar você a preparar a interface do usuário para a reprodução. Por exemplo, se você sabe que há duas faixas de áudio, é possível incluir um controle de interface do usuário que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios tiverem sido resolvidos e colocados na linha do tempo, o `MediaPlayer` será transferido para o estado PREPARADO.
1. Chame `MediaPlayer.play` para iniciar a reprodução.

O TVSDK agora inclui anúncios quando a mídia é reproduzida.