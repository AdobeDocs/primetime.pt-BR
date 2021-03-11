---
description: Os fluxos HLS que são entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação nas solicitações de manifesto e segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookies.
title: Fluxos de segmentos tokenizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Fluxos de segmento tokenized {#tokenized-segment-streams}

Os fluxos HLS que são entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação nas solicitações de manifesto e segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookies.

Tokens fornecidos como cookies na resposta do manifesto principal (m3u8) não são compartilhados com as solicitações do segmento (ts) mesmo quando as solicitações do segmento são para o mesmo domínio. Para habilitar o compartilhamento desses cookies em uma solicitação de segmento, defina a seguinte propriedade na instância `PTMetadata` fornecida ao item do player: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Uma solicitação adicional é feita ao manifesto principal (m3u8) antes que o fluxo comece a ser reproduzido.

>[!IMPORTANT]
>
>Este recurso de compartilhamento de cookies só é compatível com dispositivos que executam o iOS 8 ou superior.

