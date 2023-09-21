---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O detecta tags ID3 no nível de segmento TS (fluxo de transporte) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag.
title: Tags ID3
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Tags ID3{#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O detecta tags ID3 no nível de segmento TS (fluxo de transporte) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag.

>[!IMPORTANT]
>
>O TVSDK reconhece metadados ID3 (versão 2.3.0 ou 2.4.0) em fluxos de áudio (AAC) e vídeo (H.264), em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora tags ID3 que não estão em uma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta metadados de ID3, ele emite uma notificação com os seguintes dados:

* InfoCode = 303007
* TIPO = ID3
* NAME = ausente
* ID = 0

1. Implementar um ouvinte de eventos para `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` e registre-o com o `MediaPlayer` objeto.

   O TVSDK chama esse ouvinte quando detecta metadados de ID3.

   >[!NOTE]
   >
   >As dicas de anúncios personalizados usam o mesmo `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois dicas de anúncios personalizados são detectadas no nível do manifesto e tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte custom-tags-configure.

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
