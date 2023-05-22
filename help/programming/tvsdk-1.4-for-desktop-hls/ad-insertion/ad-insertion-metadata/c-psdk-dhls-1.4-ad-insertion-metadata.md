---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.
title: Adicionar metadados de inserção
exl-id: 83c0fd25-dbc3-4529-b81a-16ff78012c80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Adicionar metadados de inserção {#ad-insertion-metadata}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.

O TVSDK inclui a biblioteca de decisão de anúncios do Primetime. Para que seu conteúdo inclua anúncios do servidor do Primetime ad decisioning, seu aplicativo deve fornecer os seguintes itens necessários `AuditudeSettings` informações:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncio para o servidor do Adobe Primetime Ad Decisioning. Essa ID é usada pela decisão de anúncio do Primetime para recuperar informações de anúncio relacionadas ao vídeo do servidor.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de direcionamento.

   Você pode incluir esses parâmetros dependendo das suas necessidades e das necessidades do provedor de anúncios.

## Configurar metadados de inserção de anúncio {#set-up-ad-insertion-metadata}

Use a classe auxiliar AuditudeSettings, que estende a classe MetadataNode, para configurar os metadados de Adobe Primetime ad decisioning.

>[!TIP]
>
>O Adobe Primetime ad decisioning era anteriormente conhecido como Auditude.

Os metadados de publicidade estão na `MediaResource.metadata` propriedade. Ao iniciar a reprodução de um novo vídeo, seu aplicativo é responsável por definir os metadados de publicidade corretos.

1. Crie o `AuditudeSettings` instância.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Defina a mediaID, a zoneID, o domínio e os parâmetros opcionais de direcionamento do Adobe Primetime ad decisioning.

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
   >A ID de mídia é consumida pelo TVSDK como uma string, que é convertida em um valor md5, e é usada para a variável `u` valor na solicitação de URL do Primetime e da decisão. Por exemplo:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Criar um `MediaResource` usando o URL do fluxo de mídia e os metadados de publicidade criados anteriormente.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Carregue o `MediaResource` por meio do `MediaPlayer.replaceCurrentResource` método.

   A variável `MediaPlayer` inicia o carregamento e o processamento do manifesto de fluxo de mídia.

1. (Opcional) Consulte as `MediaPlayerItem` instância para ver se o fluxo está ativo, independentemente de ter faixas de áudio alternativas ou se o fluxo está protegido.

   Essas informações podem ajudar você a preparar a interface do usuário para a reprodução. Por exemplo, se você souber que existem duas faixas de áudio, poderá incluir um controle de interface do usuário que alterna entre essas faixas.

1. Chame `MediaPlayer.prepareToPlay` para iniciar o fluxo de trabalho de publicidade.

   Depois que os anúncios forem resolvidos e colocados na linha do tempo, a variável `MediaPlayer` transições para o estado PREPARADO.
1. Chame `MediaPlayer.play` para iniciar a reprodução.

O TVSDK agora inclui anúncios quando a mídia é reproduzida.
