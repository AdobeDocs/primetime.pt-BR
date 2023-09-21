---
description: Os fluxos HLS entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookie.
title: Fluxos de segmentos tokenizados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Fluxos de segmentos tokenizados{#tokenized-segment-streams}

Os fluxos HLS entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookie.

Os tokens fornecidos como cookies na resposta do manifesto principal (m3u8) não são compartilhados com as solicitações de segmento (ts), mesmo quando as solicitações de segmento são para o mesmo domínio. Para habilitar o compartilhamento desses cookies em uma solicitação de segmento, defina a seguinte propriedade no campo `PTMetadata` instância fornecida para o item de reprodutor: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Uma solicitação adicional é feita ao manifesto principal (m3u8) antes que o fluxo comece a ser reproduzido.

>[!IMPORTANT]
>
>Este recurso de compartilhamento de cookies só tem suporte em dispositivos que executam o iOS 8 ou superior.
