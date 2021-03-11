---
description: A maioria dos anunciantes requer informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram visualizados. A abordagem mais eficiente é fazer com que o reprodutor do cliente envie relatórios durante a reprodução dos anúncios, mas o servidor manifest também oferece suporte ao rastreamento de anúncios híbrido e no lado do servidor.
title: Rastreamento de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Rastreamento de anúncio {#ad-tracking}

A maioria dos anunciantes requer informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram visualizados. A abordagem mais eficiente é fazer com que o reprodutor do cliente envie relatórios durante a reprodução dos anúncios, mas o servidor manifest também oferece suporte ao rastreamento de anúncios híbrido e no lado do servidor.

Ao ativar o rastreamento de anúncios, o cliente especifica uma das seguintes abordagens:

* **Lado do cliente** Juntamente com a lista de reprodução com ponto de anúncio, o servidor envia ao cliente uma estrutura JSON, VMAP ou in-manifest especificando eventos de rastreamento e URLs. Este método é compatível com o Interative Advertising Bureau (IAB)

* **Lado do servidor** O cliente não participa do rastreamento de anúncios. O servidor envia as informações de rastreamento do anúncio que puder. Os dados de rastreamento são calculados somente no lado do servidor e podem não corresponder à atividade de reprodução no lado do cliente. Por exemplo, se um usuário final não visualizar o anúncio inteiro, depois que os segmentos forem entregues, o servidor ainda considerará o anúncio como reproduzido.

* **** HíbridoÉ como o rastreamento no lado do cliente, mas o cliente envia seus relatórios para o servidor de manifesto, que os repassa para os URLs apropriados. Os anunciantes recebem as mesmas informações que com o rastreamento do lado do cliente. Esse modo acomoda clientes que estão executando com acesso restrito à Internet.