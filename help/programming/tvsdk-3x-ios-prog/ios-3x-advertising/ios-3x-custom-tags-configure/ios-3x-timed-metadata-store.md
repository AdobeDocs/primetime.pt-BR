---
description: Seu aplicativo deve usar os objetos PTTimedMetadata apropriados nos momentos apropriados.
seo-description: Seu aplicativo deve usar os objetos PTTimedMetadata apropriados nos momentos apropriados.
seo-title: Armazenar objetos de metadados cronometrados à medida que são despachados
title: Armazenar objetos de metadados cronometrados à medida que são despachados
uuid: 38e72a9b-571a-48da-9c17-80be453e6a98
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Armazenar objetos de metadados cronometrados à medida que são despachados {#store-timed-metadata-objects-as-they-are-dispatched}

Seu aplicativo deve usar os objetos PTTimedMetadata apropriados nos momentos apropriados.

Durante a análise de conteúdo, que ocorre antes da reprodução, o TVSDK identifica as tags assinadas e notifica seu aplicativo sobre essas tags. A hora associada a cada `PTTimedMetadata` é a hora absoluta na linha do tempo de reprodução.

Seu aplicativo deve concluir as seguintes tarefas:

1. Acompanhe o tempo de reprodução atual.
1. Corresponder o tempo de reprodução atual aos objetos `PTTimedMetadata` despachados.

1. Use `PTTimedMetadata` onde a hora do start for igual à hora atual de reprodução.

   >[!NOTE]
   >
   >O código abaixo supõe que haja apenas uma instância `PTTimedMetadata` de cada vez. Se houver várias instâncias, o aplicativo deve salvá-las adequadamente em um dicionário. Um método é criar uma matriz em um determinado momento e armazenar todas as instâncias nessa matriz.

   O exemplo a seguir mostra como salvar os objetos `PTTimedMetadata` em um `NSMutableDictionary (timedMetadataCollection)` marcado pela hora do start de cada `timedMetadata`.

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

## Analisando tags Nielsen ID3 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

Para extrair a tag ID3 para análise, use o seguinte no método `onMediaPlayerSubscribedTagIdentified`:

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
