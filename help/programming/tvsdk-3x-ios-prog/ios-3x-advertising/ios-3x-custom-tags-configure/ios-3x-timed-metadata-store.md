---
description: Seu aplicativo deve usar os objetos PTTimedMetadata apropriados nos momentos apropriados.
title: Armazenar objetos de metadados cronometrados à medida que são expedidos
exl-id: 8b859e8d-eb4c-48f9-a95e-1bcc35a2a520
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Armazenar objetos de metadados cronometrados à medida que são expedidos {#store-timed-metadata-objects-as-they-are-dispatched}

Seu aplicativo deve usar os objetos PTTimedMetadata apropriados nos momentos apropriados.

Durante a análise de conteúdo, que ocorre antes da reprodução, o TVSDK identifica tags assinadas e notifica o aplicativo sobre essas tags. O tempo associado a cada `PTTimedMetadata` é o tempo absoluto na linha do tempo de reprodução.

Seu aplicativo deve concluir as seguintes tarefas:

1. Rastreie o tempo de reprodução atual.
1. Corresponder o tempo de reprodução atual ao distribuído `PTTimedMetadata` objetos.

1. Use o `PTTimedMetadata` em que a hora de início é igual à hora de reprodução atual.

   >[!NOTE]
   >
   >O código abaixo presume que há apenas um `PTTimedMetadata` instância de cada vez. Se houver várias instâncias, o aplicativo deverá salvá-las adequadamente em um dicionário. Um método é criar uma matriz em um determinado momento e armazenar todas as instâncias nessa matriz.

   O exemplo a seguir mostra como salvar `PTTimedMetadata` objetos em uma `NSMutableDictionary (timedMetadataCollection)` digitado pela hora de início de cada `timedMetadata`.

   ```
   NSMutableDictionary *timedMetadataCollection; 
   
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
   
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## Análise de tags Nielsen ID3 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

Para extrair a tag ID3 para análise, use o seguinte no `onMediaPlayerSubscribedTagIdentified` método:

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

Depois de analisar a tag ID3, extraia os metadados específicos do Nielsen usando o seguinte:

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```
