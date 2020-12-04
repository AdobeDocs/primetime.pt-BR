---
description: Você pode usar TimedMetadata quando o tempo de reprodução atual corresponder ao tempo do start.
seo-description: Você pode usar TimedMetadata quando o tempo de reprodução atual corresponder ao tempo do start.
seo-title: Usar metadados cronometrados
title: Usar metadados cronometrados
uuid: 1531780f-2502-4235-818c-6c0a6bf3d348
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# Usar metadados cronometrados {#use-timed-metadata}

Você pode usar TimedMetadata quando o tempo de reprodução atual corresponder ao tempo do start.

Para usar esses objetos salvos `PTTimedMetadata` durante a reprodução, use o dicionário salvo de [Armazenar objetos de metadados cronometrados conforme são despachados](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md).

1. Extraia e atualize o tempo de reprodução atual desta notificação e localize todos os objetos `PTTimedMetadata` com as horas de start que correspondem ao tempo de reprodução atual.

   É possível usar esses objetos para concluir várias ações.

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

1. Limpe periodicamente instâncias obsoletas `PTTimedMetadata` da lista para evitar que a memória cresça continuamente.