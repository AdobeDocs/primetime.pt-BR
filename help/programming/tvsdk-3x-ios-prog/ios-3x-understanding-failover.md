---
description: O tratamento de failover ocorre quando uma lista de reprodução variante tem várias representações para a mesma taxa de bits e uma das representações para de funcionar. O TVSDK alterna entre representações.
title: Failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Failover {#failover}

O tratamento de failover ocorre quando uma lista de reprodução variante tem várias representações para a mesma taxa de bits e uma das representações para de funcionar. O TVSDK alterna entre representações.

O exemplo a seguir mostra uma lista de reprodução variante com URLs de failover com a mesma taxa de bits:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Quando o TVSDK carrega a lista de reprodução da variante, ele cria uma fila que armazena os URLs de todas as representações do conteúdo para a mesma taxa de bits. Quando uma solicitação de um URL falha, o TVSDK usa o próximo URL com a mesma taxa de bits da fila de failover. Em qualquer momento de falha específico, o TVSDK percorre todos os URLs disponíveis uma vez até encontrar um que funcione corretamente ou até tentar todos os URLs disponíveis. Se o TVSDK tentou reproduzir todos os URLs disponíveis e nenhum deles funcionou, o TVSDK para de tentar reproduzir o conteúdo.

O failover ocorre somente no nível M3U8, o que significa:

* Para VOD, o failover só pode ocorrer quando ele começa a tentar reproduzir e não depois de ter começado a reproduzir.
* Para transmissão ao vivo, o failover pode ocorrer no meio da transmissão.

>[!TIP]
>
>O TVSDK, em vez do reprodutor Apple AV Foundation, fornece o tratamento de failover.
