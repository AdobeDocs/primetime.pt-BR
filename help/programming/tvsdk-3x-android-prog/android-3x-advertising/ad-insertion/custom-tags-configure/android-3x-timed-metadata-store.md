---
description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
seo-description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
seo-title: Armazenar objetos de metadados cronometrados à medida que são despachados
title: Armazenar objetos de metadados cronometrados à medida que são despachados
uuid: 3d0ed022-829d-474e-83a9-152caeb5b317
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Armazenar objetos de metadados cronometrados à medida que são despachados {#store-timed-metadata-objects-as-they-are-dispatched}

Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.

Durante a análise de conteúdo, que ocorre antes da reprodução, o TVSDK identifica as tags assinadas e notifica seu aplicativo sobre essas tags.

>[!TIP]
>
>A hora associada a cada `TimedMetadata` é a hora local na linha do tempo de reprodução.

Para armazenar objetos de metadados cronometrados à medida que são despachados:

1. Acompanhe o tempo de reprodução atual.
1. Corresponder o tempo de reprodução atual aos objetos `TimedMetadata` despachados.

1. Use `TimedMetadata` onde a hora do start for igual à hora atual de reprodução local.

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

