---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O detecta tags ID3 no nível de segmento do fluxo de transporte (TS) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
title: Tags ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Tags ID3{#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O detecta tags ID3 no nível de segmento do fluxo de transporte (TS) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .

>[!IMPORTANT]
>
>O TVSDK reconhece os metadados ID3 (versão 2.3.0 ou 2.4.0) em fluxos de áudio (AAC) e vídeo (H.264), em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora as tags ID3 que não estão em uma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta metadados ID3, ele emite uma notificação com os seguintes dados:

* InfoCode = 303007
* TYPE = ID3
* NAME = não presente
* ID = 0

1. Implemente um ouvinte de evento para `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` e registre-o no objeto `MediaPlayer` .

   O TVSDK chama esse ouvinte quando detecta metadados ID3.

   >[!NOTE]
   >
   >As dicas de anúncio personalizadas usam o mesmo evento `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão porque as dicas de anúncio personalizadas são detectadas no nível de manifesto e as tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte personalizar tags-configure .

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

