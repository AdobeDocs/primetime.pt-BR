---
description: As solicitações do cliente para inserção de anúncio normalmente especificam mais de uma taxa de bits na lista de reprodução de variante formatada em M3U8. O servidor manifest gera e retorna um novo arquivo de variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Também gera uma ID de grupo exclusiva para unir esses M3U8s.
title: Fluxos de taxa de bits múltipla
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Fluxos de taxa de bits múltipla {#multiple-bit-rate-streams}

As solicitações do cliente para inserção de anúncio normalmente especificam mais de uma taxa de bits na lista de reprodução de variante formatada em M3U8. O servidor manifest gera e retorna um novo arquivo de variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Também gera uma ID de grupo exclusiva para unir esses M3U8s.

O servidor manifest usa as informações na solicitação do URL do Bootstrap do cliente para recuperar a lista de reprodução da variante de conteúdo. Ele gera uma nova lista de reprodução de variante contendo links de servidor de manifesto para o conteúdo no nível do fluxo. O cliente os usa para criar solicitações de inserção de anúncio. Os links de conteúdo no nível de fluxo do servidor de manifesto têm o seguinte formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** O servidor de manifesto define esse valor com base no tipo de lista de reprodução do conteúdo: Ao vivo/linear (#EXT-X-PLAYLIST-TYPE:EVENT) ou VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** A ID exclusiva do editor para o conteúdo específico fornecido na solicitação de URL do Bootstrap.

* **`rendition`** O servidor de manifesto define isso com base no valor BANDWIDTH do fluxo de conteúdo e o usa para corresponder a taxa de bits do anúncio à taxa de bits do conteúdo. A taxa de bits do anúncio não pode exceder a taxa de bits do conteúdo, a menos que a renderização do anúncio com a taxa de bits mais baixa o faça.

* **`groupID`** O servidor de manifesto gera esse valor e o usa para garantir que ele coloque anúncios de forma consistente, independentemente de qual taxa de bits representará os anúncios do cliente.

* **`base64-encoded url of the bit rate stream`** A base64 segura para URL do servidor de manifesto codifica o URL absoluto do fluxo de conteúdo. Cada fluxo tem seu próprio URL.

* **`Query parameters`** Parâmetros de consulta fornecidos na solicitação de URL do Bootstrap.

