---
description: O aplicativo deve usar os objetos TimedMetadata apropriados em momentos apropriados.
title: Armazenar objetos de metadados cronometrados à medida que são despachados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Armazenar objetos de metadados cronometrados à medida que são despachados {#store-timed-metadata-objects-as-they-are-dispatched}

O aplicativo deve usar os objetos TimedMetadata apropriados em momentos apropriados.

Durante a análise de conteúdo, o que acontece antes da reprodução, o TVSDK identifica as tags assinadas e notifica seu aplicativo sobre essas tags. O tempo associado a cada `TimedMetadata` é o horário local na linha do tempo da reprodução.

O aplicativo deve realizar as seguintes tarefas:

1. Rastreie o tempo de reprodução atual.
1. Corresponda o tempo de reprodução atual aos objetos `TimedMetadata` despachados.

1. Use `TimedMetadata` onde a hora de início é igual à hora de reprodução local atual.

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

