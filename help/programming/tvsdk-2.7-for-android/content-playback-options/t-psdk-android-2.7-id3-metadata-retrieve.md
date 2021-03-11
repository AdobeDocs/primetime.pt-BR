---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível de segmento do fluxo de transporte (TS) em fluxos de HLS e despacha um evento. O aplicativo pode extrair dados da tag .
title: Tags ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Tags ID3 {#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível de segmento do fluxo de transporte (TS) em fluxos de HLS e despacha um evento. O aplicativo pode extrair dados da tag .

>[!IMPORTANT]
>
>O TVSDK reconhece os metadados ID3 (versão 2.3.0 ou 2.4.0) em fluxos de áudio (AAC) e vídeo (H.264) em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora as tags ID3 que não estão em uma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta metadados ID3, ele emite uma notificação com os seguintes dados:

* TYPE = ID3
* NAME = ID3

1. Implemente um ouvinte de evento para `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registre-o no objeto `MediaPlayer` .

   O TVSDK chama esse ouvinte quando detecta metadados `ID3`.

   >[!TIP]
   >
   >As dicas de anúncio personalizadas usam o mesmo evento `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão porque as dicas de anúncio personalizadas são detectadas no nível de manifesto e as tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte [Tags personalizadas](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


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

