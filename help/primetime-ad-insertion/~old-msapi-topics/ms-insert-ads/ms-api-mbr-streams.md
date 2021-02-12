---
description: As solicitações do cliente para inserção de publicidade normalmente especificam mais de uma taxa de bits na lista de reprodução formatado M3U8 variante. O servidor manifest gera e retorna um novo arquivo de variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Também gera uma ID de grupo exclusiva para unir esses M3U8s.
seo-description: As solicitações do cliente para inserção de publicidade normalmente especificam mais de uma taxa de bits na lista de reprodução formatado M3U8 variante. O servidor manifest gera e retorna um novo arquivo de variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Também gera uma ID de grupo exclusiva para unir esses M3U8s.
seo-title: Vários fluxos de taxa de bits
title: Vários fluxos de taxa de bits
uuid: f59cb765-e000-43e0-8d3a-8149a3c5b96e
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Vários fluxos de taxa de bits {#multiple-bit-rate-streams}

As solicitações do cliente para inserção de publicidade normalmente especificam mais de uma taxa de bits na lista de reprodução formatado M3U8 variante. O servidor manifest gera e retorna um novo arquivo de variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Também gera uma ID de grupo exclusiva para unir esses M3U8s.

O servidor manifest usa as informações na solicitação do URL do Bootstrap do cliente para recuperar a lista de reprodução da variante de conteúdo. Ele gera uma nova lista de reprodução variante que contém links de servidor manifest para o conteúdo no nível do fluxo. O cliente os usa para construir solicitações de inserção de anúncios. Os links de conteúdo em nível de fluxo do servidor manifest têm o seguinte formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** O servidor manifest define esse valor com base no tipo de lista de reprodução do conteúdo: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENTO) ou VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** A ID exclusiva do editor para o conteúdo específico fornecido na solicitação de URL do Bootstrap.

* **`rendition`** O servidor manifest define isso com base no valor BANDWIDTH do fluxo de conteúdo e o usa para corresponder a taxa de bits do anúncio à taxa de bits do conteúdo. A taxa de bits do anúncio não pode exceder a taxa de bits do conteúdo, a menos que a execução do anúncio com a menor taxa de bits o faça.

* **`groupID`** O servidor manifest gera esse valor e o usa para garantir que coloque os anúncios de forma consistente, independentemente da taxa de bits que o cliente solicita os anúncios.

* **`base64-encoded url of the bit rate stream`** A base64 segura para URL do servidor manifest codifica o URL absoluto do fluxo de conteúdo. Cada fluxo tem seu próprio URL.

* **`Query parameters`** Parâmetros de query fornecidos na solicitação de URL do Bootstrap.

