---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
seo-description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .
seo-title: Tags ID3
title: Tags ID3
uuid: 3fa199cd-668d-4d26-928f-074b6114b84c
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Tags ID3 {#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível do segmento de fluxo de transporte (TS) nos fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag .

>[!IMPORTANT]
>
>O TVSDK reconhece os metadados ID3 (versão 2.3.0 ou 2.4.0) nos fluxos de áudio (AAC) e vídeo (H.264) em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora as tags ID3 que não estão em nenhuma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta os metadados ID3, ele emite uma notificação com os seguintes dados:

* TYPE = ID3
* NAME = ID3

1. Implemente um ouvinte de evento para `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registre-o no `MediaPlayer` objeto.

   O TVSDK chama esse ouvinte quando detecta `ID3` metadados.

   >[!TIP]
   >
   >As dicas de anúncio personalizadas usam o mesmo `onTimedMetadata` evento para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois as dicas de anúncio personalizadas são detectadas no nível do manifesto e as tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte Tags [personalizadas](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


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
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```

