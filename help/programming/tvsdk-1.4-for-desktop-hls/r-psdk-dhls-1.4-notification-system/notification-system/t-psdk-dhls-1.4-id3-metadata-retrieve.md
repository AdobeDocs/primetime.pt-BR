---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. detecta as tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
seo-description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. detecta as tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
seo-title: Tags ID3
title: Tags ID3
uuid: 5c016260-5ced-480e-897a-11ffe7f34441
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Tags ID3{#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. detecta as tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .

>[!IMPORTANT]
>
>O TVSDK reconhece os metadados ID3 (versão 2.3.0 ou 2.4.0) nos fluxos de áudio (AAC) e vídeo (H.264), em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora as tags ID3 que não estão em nenhuma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta os metadados ID3, ele emite uma notificação com os seguintes dados:

* InfoCode = 303007
* TYPE = ID3
* NAME = não presente
* ID = 0

1. Implemente um ouvinte de evento para `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` e registre-o com o objeto `MediaPlayer`.

   O TVSDK chama esse ouvinte quando detecta metadados ID3.

   >[!NOTE]
   >
   >As dicas de anúncio personalizadas usam o mesmo evento `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois as dicas de anúncio personalizadas são detectadas no nível do manifesto e as tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte custom-tags-configure .

1. Recupere os metadados.

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```

