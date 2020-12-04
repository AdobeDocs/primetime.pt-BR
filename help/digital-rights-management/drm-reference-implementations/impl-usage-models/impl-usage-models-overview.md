---
description: nulo
seo-description: nulo
seo-title: Visão geral
title: Visão geral
uuid: 5f82f603-6e2d-4c9d-a49f-7b07f30a29e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Visão geral{#overview}

A Implementação de referência inclui uma opção de modo de demonstração que demonstra como implementar diferentes modelos de uso para um segmento de conteúdo empacotado. O modo de demonstração apresenta lógica comercial para estes modelos de uso:

* **Download por conta própria (DTO)**  - Os usuários podem baixar o conteúdo online ou offline e recebem uma licença permanente para o conteúdo.
* **Aluguer/VOD (Video-On-Demand)**  - O conteúdo disponível é fornecido com restrições baseadas em tempo. Por exemplo, os usuários podem reproduzir conteúdo durante um período de 30 dias. Quando a reprodução é iniciada, o usuário tem até 48 horas para terminar de assistir ao conteúdo. O conteúdo deve ser exibido em 30 dias.
* **Subscrição (tudo o que você pode comer)**  - Alguns serviços ofertas subscrições pagas que concedem aos usuários acesso ilimitado a uma grande biblioteca de conteúdo, desde que continuem pagando uma taxa mensal. O servidor de licenças emite uma licença exclusiva para cada segmento de conteúdo e também emite uma licença raiz que expira no final do período de subscrição. Todos os meses, quando os usuários renovam suas subscrições, a licença raiz também deve ser renovada.

   >[!NOTE]
   >
   >Para os modelos de uso anteriores, após adquirir uma licença, os usuários devem digitar suas credenciais para que o servidor possa verificar se os usuários têm uma conta de aluguel.

* **Financiamento**  de anúncios - o conteúdo é monetizado pela inclusão de anúncios como parte da experiência. Com esse modelo, o conteúdo pode ser distribuído e não requer autenticação do usuário.

No modo de demonstração do modelo de uso, a lógica comercial no servidor controla os atributos das licenças geradas. No momento do empacotamento, sua política de DRM deve indicar apenas se a autenticação é necessária.

Para ativar todos os quatro modelos de uso, é necessário incluir apenas duas políticas de DRM:

* Uma política de DRM que permite o acesso anônimo ao modelo financiado pelo anúncio
* Uma política DRM que requer autenticação de nome de usuário/senha para os outros três modelos de uso.

Quando um usuário solicita uma licença, um aplicativo cliente pode determinar se deve solicitar a autenticação ao usuário com base nas informações de autenticação nas políticas de DRM.
