---
description: A manipulação de failover ocorre quando uma lista de reprodução de variante tem várias representações para a mesma taxa de bits e uma das representações para de funcionar. O TVSDK alterna entre representações.
title: Failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Failover {#failover}

A manipulação de failover ocorre quando uma lista de reprodução de variante tem várias representações para a mesma taxa de bits e uma das representações para de funcionar. O TVSDK alterna entre representações.

O exemplo a seguir mostra uma lista de reprodução de variante com URLs de failover da mesma taxa de bits:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Quando o TVSDK carrega a lista de reprodução da variante, ela cria uma fila que armazena os URLs para todas as representações do conteúdo para a mesma taxa de bits. Quando uma solicitação de URL falha, o TVSDK usa o próximo URL da mesma taxa de bits da fila de failover. Em qualquer momento de falha específico, o TVSDK percorre todos os URLs disponíveis uma vez até encontrar um que funcione corretamente ou até ter tentado todos os URLs disponíveis. Se o TVSDK tentou todos os URLs disponíveis e nenhum dos URLs funcionar, o TVSDK para de tentar reproduzir o conteúdo.

O failover ocorre somente no nível M3U8, o que significa:

* Para VOD, o failover só pode ocorrer quando ele começa a tentar reproduzir e não depois de começar a reproduzir.
* Para transmissão ao vivo, o failover pode ocorrer no meio do fluxo.

>[!TIP]
>
>O TVSDK, em vez do reprodutor da Apple AV Foundation, fornece tratamento de failover.