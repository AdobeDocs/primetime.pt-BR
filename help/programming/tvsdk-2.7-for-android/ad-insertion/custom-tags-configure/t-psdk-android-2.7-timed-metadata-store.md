---
description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
seo-description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
seo-title: Armazenar objetos de metadados cronometrados à medida que são despachados
title: Armazenar objetos de metadados cronometrados à medida que são despachados
uuid: 0d0ddfea-6f32-467d-91bc-f18ceadcd842
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Armazenar objetos de metadados cronometrados à medida que são despachados {#store-timed-metadata-objects-as-they-are-dispatched}

Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.

Durante a análise de conteúdo, que ocorre antes da reprodução, o TVSDK identifica as tags assinadas e notifica seu aplicativo sobre essas tags.

>[!TIP]
>
>A hora associada a cada um `TimedMetadata` é a hora local na linha do tempo de reprodução.

Para armazenar objetos de metadados cronometrados à medida que são despachados:

1. Acompanhe o tempo de reprodução atual.
1. Corresponder o tempo de reprodução atual aos `TimedMetadata` objetos despachados.

1. Use o `TimedMetadata` local onde a hora de início é igual à hora de reprodução local atual.

   O exemplo a seguir mostra como salvar `TimedMetadata` objetos em um `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

