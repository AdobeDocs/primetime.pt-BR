---
description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
seo-description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
seo-title: Armazenar objetos de metadados cronometrados à medida que são despachados
title: Armazenar objetos de metadados cronometrados à medida que são despachados
uuid: 0e6d2a42-37a8-477e-b925-66bbc23445c1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Armazenar objetos de metadados cronometrados à medida que são despachados {#store-timed-metadata-objects-as-they-are-dispatched}

Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.

Durante a análise de conteúdo, que ocorre antes da reprodução, o TVSDK identifica as tags assinadas e notifica seu aplicativo sobre essas tags. A hora associada a cada um `TimedMetadata` é a hora local na linha do tempo de reprodução.

Seu aplicativo deve concluir as seguintes tarefas:

1. Acompanhe o tempo de reprodução atual.
1. Corresponder o tempo de reprodução atual aos `TimedMetadata` objetos despachados.

1. Use o `TimedMetadata` local onde a hora de início é igual à hora de reprodução local atual.

   O exemplo a seguir mostra como salvar `TimedMetadata` objetos em um `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

