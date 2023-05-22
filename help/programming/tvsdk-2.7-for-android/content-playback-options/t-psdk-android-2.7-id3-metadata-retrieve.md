---
description: As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível de segmento de fluxo de transporte (TS) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag.
title: Tags ID3
exl-id: 316bc704-e71a-4fd7-b970-706b8c08a42e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Tags ID3 {#id-tags}

As tags ID3 fornecem informações sobre um arquivo de áudio ou vídeo, como o título do arquivo ou o nome do artista. O TVSDK detecta tags ID3 no nível de segmento de fluxo de transporte (TS) em fluxos HLS e despacha um evento. O aplicativo pode extrair dados da tag.

>[!IMPORTANT]
>
>O TVSDK reconhece metadados ID3 (versão 2.3.0 ou 2.4.0) em fluxos de áudio (AAC) e vídeo (H.264) em qualquer uma de suas possíveis codificações (ASCII, UTF8, UTF16-BE ou UTF16-LE). Ele ignora tags ID3 que não estão em uma das versões ou formatos reconhecidos. A codificação não especificada é tratada como UTF8.

Quando o TVSDK detecta metadados de ID3, ele emite uma notificação com os seguintes dados:

* TIPO = ID3
* NOME = ID3

1. Implementar um ouvinte de eventos para `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` e registre-o com o `MediaPlayer` objeto.

   O TVSDK chama esse ouvinte quando detecta `ID3` metadados.

   >[!TIP]
   >
   >As dicas de anúncios personalizados usam o mesmo `onTimedMetadata` para indicar a detecção de uma nova tag. Isso não deve causar confusão, pois dicas de anúncios personalizados são detectadas no nível do manifesto e tags ID3 são incorporadas no fluxo. Para obter mais informações, consulte [Tags personalizadas](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


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
