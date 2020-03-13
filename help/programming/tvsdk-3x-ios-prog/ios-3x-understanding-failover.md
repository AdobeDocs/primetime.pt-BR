---
description: A manipulação de failover ocorre quando uma lista de reprodução variante tem várias execuções para a mesma taxa de bits, e uma das execuções para de funcionar. O TVSDK alterna entre execuções.
seo-description: A manipulação de failover ocorre quando uma lista de reprodução variante tem várias execuções para a mesma taxa de bits, e uma das execuções para de funcionar. O TVSDK alterna entre execuções.
seo-title: Failover
title: Failover
uuid: 064886ab-afa2-4afc-b795-d094b31934b8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Failover {#failover}

A manipulação de failover ocorre quando uma lista de reprodução variante tem várias execuções para a mesma taxa de bits, e uma das execuções para de funcionar. O TVSDK alterna entre execuções.

O exemplo a seguir mostra uma lista de reprodução variante com URLs de failover da mesma taxa de bits:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Quando o TVSDK carrega a lista de reprodução variante, ela cria uma fila que armazena os URLs de todas as execuções do conteúdo para a mesma taxa de bits. Quando uma solicitação de um URL falha, o TVSDK usa o próximo URL da mesma taxa de bits da fila de failover. Em qualquer momento de falha específico, o TVSDK percorre todos os URLs disponíveis até encontrar um que funcione corretamente ou até tentar todos os URLs disponíveis. Se o TVSDK tentou todos os URLs disponíveis e nenhum deles funcionar, o TVSDK para de tentar reproduzir o conteúdo.

O failover ocorre somente no nível M3U8, o que significa:

* Para VOD, o failover só pode ocorrer quando começa a tentar reproduzir e não depois que a reprodução é iniciada.
* Para transmissão ao vivo, o failover pode ocorrer no meio do fluxo.

>[!TIP]
>
>O TVSDK, em vez do reprodutor do Apple AV Foundation, fornece tratamento de failover.