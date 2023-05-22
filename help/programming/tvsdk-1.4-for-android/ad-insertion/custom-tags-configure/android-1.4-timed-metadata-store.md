---
description: Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.
title: Armazenar objetos de metadados cronometrados à medida que são expedidos
exl-id: db8b303a-441e-4cc0-a80d-dc9afda482b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Armazenar objetos de metadados cronometrados à medida que são expedidos {#store-timed-metadata-objects-as-they-are-dispatched}

Seu aplicativo deve usar os objetos TimedMetadata apropriados nos momentos apropriados.

Durante a análise de conteúdo, que ocorre antes da reprodução, o TVSDK identifica tags assinadas e notifica o aplicativo sobre essas tags. O tempo associado a cada `TimedMetadata` é a hora local na linha do tempo de reprodução.

Seu aplicativo deve concluir as seguintes tarefas:

1. Rastreie o tempo de reprodução atual.
1. Corresponder o tempo de reprodução atual ao distribuído `TimedMetadata` objetos.

1. Use o `TimedMetadata` em que a hora de início é igual à hora atual de reprodução local.

   O exemplo a seguir mostra como salvar `TimedMetadata` objetos em uma `ArrayList`.

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
