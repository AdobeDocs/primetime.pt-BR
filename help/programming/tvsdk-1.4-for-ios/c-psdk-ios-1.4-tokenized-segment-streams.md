---
description: Os fluxos HLS entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação. Esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookie.
title: Fluxos de segmentos tokenizados
exl-id: 20a3e8a2-2e9d-4c0d-abea-66edcbcf0003
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
