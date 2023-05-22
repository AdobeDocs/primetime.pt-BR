---
description: A maioria dos anunciantes requer algumas informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram visualizados. A abordagem mais eficiente é fazer com que o player do cliente envie relatórios à medida que reproduz os anúncios, mas o servidor de manifesto também oferece suporte ao rastreamento de anúncios híbridos e do lado do servidor.
title: Rastreamento de anúncios
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Rastreamento de anúncios {#ad-tracking}

A maioria dos anunciantes requer algumas informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram visualizados. A abordagem mais eficiente é fazer com que o player do cliente envie relatórios à medida que reproduz os anúncios, mas o servidor de manifesto também oferece suporte ao rastreamento de anúncios híbridos e do lado do servidor.

Ao ativar o rastreamento de anúncios, o cliente especifica uma das seguintes abordagens:

* **Lado do cliente** Juntamente com a lista de reprodução compilada por anúncio, o servidor envia ao cliente uma estrutura JSON, VMAP ou no manifesto, especificando eventos de rastreamento e URLs. Este método é compatível com o Interative Advertising Bureau (IAB)

* **Lado do servidor** O cliente não participa do rastreamento de anúncios. O servidor envia todas as informações de rastreamento de anúncios que puder. Os dados de rastreamento são calculados somente no lado do servidor e podem não corresponder à atividade de reprodução no lado do cliente. Por exemplo, se um usuário final não visualizar todo o anúncio, depois que os segmentos forem entregues, o servidor ainda considerará o anúncio a ser reproduzido.

* **Híbrido** É como o rastreamento do lado do cliente, mas o cliente envia seus relatórios para o servidor de manifesto, que os retransmite para os URLs apropriados. Os anunciantes recebem as mesmas informações que com o rastreamento do lado do cliente. Esse modo acomoda clientes que executam com acesso restrito à Internet.