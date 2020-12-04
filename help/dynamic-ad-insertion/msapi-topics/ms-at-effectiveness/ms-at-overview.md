---
description: A maioria dos anunciantes requer algumas informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram exibidos. A abordagem mais eficiente é fazer com que o player cliente envie relatórios conforme reproduz os anúncios, mas o servidor manifest também oferece suporte ao rastreamento de anúncios híbrido e no servidor.
seo-description: A maioria dos anunciantes requer algumas informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram exibidos. A abordagem mais eficiente é fazer com que o player cliente envie relatórios conforme reproduz os anúncios, mas o servidor manifest também oferece suporte ao rastreamento de anúncios híbrido e no servidor.
seo-title: Rastreamento de anúncios
title: Rastreamento de anúncios
uuid: 184b8c36-5e51-42a7-b905-53f2b7b15e49
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Rastreamento de anúncios {#ad-tracking}

A maioria dos anunciantes requer algumas informações detalhadas sobre quando, por quanto tempo e com que sucesso seus anúncios foram exibidos. A abordagem mais eficiente é fazer com que o player cliente envie relatórios conforme reproduz os anúncios, mas o servidor manifest também oferece suporte ao rastreamento de anúncios híbrido e no servidor.

Ao ativar o rastreamento de anúncios, o cliente especifica uma das seguintes abordagens:

* **Ao** lado do clienteJuntamente com a lista de reprodução com pontos de anúncio, o servidor envia ao cliente uma estrutura JSON, VMAP ou in-manifest especificando eventos de rastreamento e URLs. Este método é compatível com o Interative Advertising Bureau (IAB)

* **Servidor** ladoO cliente não participa do rastreamento de anúncios. O servidor envia todas as informações de rastreamento de anúncios que puder. Os dados de rastreamento são calculados somente no lado do servidor e podem não corresponder à atividade de reprodução no lado do cliente. Por exemplo, se um usuário final não visualização todo o anúncio, depois que os segmentos são entregues, o servidor ainda considera o anúncio reproduzido.

* **** HíbridoÉ como o rastreamento do lado do cliente, mas o cliente envia seus relatórios para o servidor manifest, que os transmite para os URLs apropriados. Os anunciantes recebem as mesmas informações do rastreamento do lado do cliente. Este modo acomoda clientes que executam com acesso restrito à Internet.