---
description: Você pode usar TimedMetadata quando a hora atual da reprodução corresponder à hora inicial.
title: Usar metadados cronometrados
exl-id: 19375158-3647-4d6e-a2fb-6b06a2fd23c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Usar metadados cronometrados{#use-timed-metadata}

Você pode usar TimedMetadata quando a hora atual da reprodução corresponder à hora inicial.

Para usar essas `PTTimedMetadata` objetos durante a reprodução, use o dicionário salvo de [Armazenar objetos de metadados cronometrados conforme são despachados](../../../tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-timed-metadata-store.md).

1. Extrair e atualizar o tempo de reprodução atual desta notificação e localizar todos os `PTTimedMetadata` objetos com horas de início que correspondem à hora de reprodução atual.

   Você pode usar esses objetos para concluir várias ações.

   Por exemplo:

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) 
       { 
           int currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
           NSArray *allKeys = timedMetadataCollection ? [timedMetadataCollection allKeys] : [NSArray array]; 
           NSMutableArray *timedMetadatasToDelete = [[[NSMutableArray alloc] init] autorelease]; 
           int count = [allKeys count]; 
   
           for (int i=count - 1; i > -1; i--) 
           { 
              NSNumber *currTimedMetadataTime = allKeys[i]; 
              if ([currTimedMetadataTime integerValue] == currentTime) 
              { 
               /* 
                   Use the timed metadata here and remove it from the collection. 
               */ 
                NSLog (@"IN PLAYBACK TIME %i TO EXECUTE TIMEDMETADATA %@ scheduled at time %f",currentTime,currTimedMetadata.name,CMTimeGetSeconds(currTimedMetadata.time)); 
   
               PTTimedMetadata *currTimedMetadata = [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
               [timedMetadatasToDelete addObject:currTimedMetadataTime]; 
              } 
           } 
   
           for (int i=0; i<[timedMetadatasToDelete count]; i++) 
           { 
               NSNumber *timedMetadataToDelete = timedMetadatasToDelete[i]; 
               [timedMetadataCollection removeObjectForKey:timedMetadataToDelete]; 
           } 
       } 
   }
   ```

1. Liberar periodicamente arquivos obsoletos `PTTimedMetadata` instâncias da lista para evitar que a memória cresça continuamente.
