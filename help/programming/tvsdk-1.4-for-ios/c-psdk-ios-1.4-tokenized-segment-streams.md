---
description: Os fluxos HLS que são entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookie.
seo-description: Os fluxos HLS que são entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookie.
seo-title: Fluxos de segmentos Tokenized
title: Fluxos de segmentos Tokenized
uuid: b17bb5bc-2029-4113-ac44-b1d30aa08ca6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fluxos de segmentos Tokenized{#tokenized-segment-streams}

Os fluxos HLS que são entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookie.

Tokens fornecidos como cookies na resposta do manifesto mestre (m3u8) não são compartilhados com as solicitações de segmento, mesmo quando as solicitações de segmento são do mesmo domínio. Para habilitar o compartilhamento desses cookies em uma solicitação de segmento, defina a seguinte propriedade na `PTMetadata` instância fornecida ao item do player:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

É feita uma solicitação adicional ao manifesto mestre (m3u8) antes que o fluxo comece a ser reproduzido.

>[!IMPORTANT]
>
>Este recurso de compartilhamento de cookies só é suportado em dispositivos com iOS 8 ou superior.

