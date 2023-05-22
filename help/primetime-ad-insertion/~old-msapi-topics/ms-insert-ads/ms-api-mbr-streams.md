---
description: As solicitações do cliente para inserção de anúncio normalmente especificam mais de uma taxa de bits na lista de reprodução formatada M3U8 da variante. O servidor de manifesto gera e retorna um novo arquivo variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Ele também gera um identificador de grupo exclusivo para unir esses M3U8s.
title: Vários fluxos de taxa de bits
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Vários fluxos de taxa de bits {#multiple-bit-rate-streams}

As solicitações do cliente para inserção de anúncio normalmente especificam mais de uma taxa de bits na lista de reprodução formatada M3U8 da variante. O servidor de manifesto gera e retorna um novo arquivo variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Ele também gera um identificador de grupo exclusivo para unir esses M3U8s.

O servidor de manifesto usa as informações na solicitação de URL do Bootstrap do cliente para recuperar a lista de reprodução de variantes de conteúdo. Ele gera uma nova lista de reprodução variante contendo links de servidor manifest para o conteúdo em nível de fluxo. O cliente os usa para criar solicitações de inserção de anúncios. Os links de conteúdo no nível do fluxo do servidor de manifesto têm o seguinte formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** O servidor de manifesto define esse valor com base no tipo de lista de reprodução do conteúdo: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENT) ou VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** Identificador exclusivo do editor para o conteúdo específico fornecido na solicitação de URL do Bootstrap.

* **`rendition`** O servidor de manifesto define isso com base no valor BANDWIDTH do fluxo de conteúdo e o usa para corresponder a taxa de bits do anúncio à taxa de bits do conteúdo. A taxa de bits de anúncio não pode exceder a taxa de bits do conteúdo, a menos que a representação de anúncio com a taxa de bits mais baixa o faça.

* **`groupID`** O servidor de manifesto gera esse valor e o usa para garantir que ele insira anúncios de forma consistente, independentemente da taxa de bits das representações que o cliente solicita.

* **`base64-encoded url of the bit rate stream`** A base64 segura para URL do servidor de manifesto codifica a URL absoluta do fluxo de conteúdo. Cada fluxo tem seu próprio URL.

* **`Query parameters`** Parâmetros de consulta fornecidos na solicitação de URL do Bootstrap.

