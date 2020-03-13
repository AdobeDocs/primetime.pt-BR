---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
seo-description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
seo-title: Tags ID3
title: Tags ID3
uuid: 5e5c5f89-7653-47c1-b9c1-6b9b9b1f8d73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Tags ID3 {#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .

>[!IMPORTANT]
>
>O TVSDK reconhece os metadados ID3 (versão 2.3.0 ou 2.4.0) nos fluxos de áudio (AAC) e vídeo (H.264), em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora as tags ID3 que não estão em nenhuma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta os metadados ID3, ele emite uma notificação com os seguintes dados:

* InfoCode = 303007
* TYPE = ID3
* NAME = não presente
* ID = 0

1. Implemente um ouvinte de evento para `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registre-o no `MediaPlayer` objeto.

   O TVSDK chama esse ouvinte quando detecta metadados ID3.

   >[!NOTE]
   >
   >As dicas de anúncio personalizadas usam o mesmo `onTimedMetadata` evento para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois as dicas de anúncio personalizadas são detectadas no nível do manifesto e as tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte custom-tags-configure .

1. Recupere os metadados.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```

