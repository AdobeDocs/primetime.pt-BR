---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.
seo-description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.
seo-title: Metadados de inserção de anúncio
title: Metadados de inserção de anúncio
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Metadados de inserção de anúncio {#ad-insertion-metadata}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.

O TVSDK inclui a biblioteca de decisão de anúncio Primetime. Para que seu conteúdo inclua anúncios do servidor de decisão do anúncio Primetime, seu aplicativo deve fornecer as seguintes informações `AuditudeSettings` necessárias:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncios ao servidor de decisão de publicidade da Adobe Primetime. Essa ID é usada pela decisão do anúncio Primetime para recuperar informações relacionadas ao anúncio do vídeo do servidor.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

   Você pode incluir esses parâmetros, dependendo de suas necessidades e das necessidades do provedor de publicidade.

## Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de decisão de anúncio do Adobe Primetime.

>[!TIP]
>
>A decisão do anúncio da Adobe Primetime era anteriormente conhecida como Auditude.

Os metadados de publicidade estão na propriedade `MediaResource.metadata`. Ao iniciar a reprodução de um novo vídeo, seu aplicativo é responsável por definir os metadados de publicidade corretos.

1. Crie a instância `AuditudeSettings`.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Defina a ID de mídia de decisão de publicidade da Adobe Primetime, zoneID, domínio e os parâmetros de definição de metas opcionais.

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
   >A ID de mídia é consumida pelo TVSDK como uma string, que é convertida em um valor md5 e é usada para o valor `u` na solicitação de URL de decisão do Primetime ad. Por exemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crie uma instância `MediaResource` usando o URL de fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Carregue o objeto `MediaResource` pelo método `MediaPlayer.replaceCurrentResource`.

   O `MediaPlayer` start o carregamento e o processamento do manifesto de fluxo de mídia.

1. (Opcional) Query a instância `MediaPlayerItem` para ver se o fluxo é ao vivo, independentemente de ter faixas de áudio alternativas ou se o fluxo é protegido.

   Estas informações podem ajudá-lo a preparar a interface para a reprodução. Por exemplo, se você sabe que existem duas faixas de áudio, é possível incluir um controle de interface que alterne entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para start do fluxo de trabalho de publicidade.

   Depois que as publicidades forem resolvidas e colocadas na linha do tempo, a `MediaPlayer` transição para o estado PREPARADO.
1. Chame `MediaPlayer.play` para start da reprodução.

O TVSDK agora inclui anúncios quando sua mídia é reproduzida.