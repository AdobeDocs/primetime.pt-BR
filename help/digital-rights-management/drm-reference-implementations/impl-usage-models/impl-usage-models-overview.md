---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Visão geral{#overview}

A Implementação de referência inclui uma opção de modo de demonstração que demonstra como implementar diferentes modelos de uso para um segmento de conteúdo empacotado. O modo de demonstração apresenta uma lógica de negócios para estes modelos de uso:

* **Download por conta própria (DTO)**  - os usuários podem baixar o conteúdo online ou offline e recebem uma licença permanente para o conteúdo.
* **Aluguel/vídeo sob demanda (VOD)**  - O conteúdo disponível vem com restrições baseadas em tempo. Por exemplo, os usuários podem reproduzir o conteúdo durante um período de 30 dias. Quando a reprodução começar, o usuário terá até 48 horas para terminar de assistir ao conteúdo. O conteúdo deve ser exibido em 30 dias.
* **Assinatura (tudo o que você pode comer)**  - Alguns serviços oferecem assinaturas pagas que dão aos usuários acesso ilimitado a uma grande biblioteca de conteúdo, desde que continuem pagando uma taxa mensal. O servidor de licenças emite uma licença exclusiva para cada segmento de conteúdo e também emite uma licença raiz que expira ao final do período de assinatura. A cada mês, quando os usuários renovam sua assinatura, a licença raiz também deve ser renovada.

   >[!NOTE]
   >
   >Para os modelos de uso anteriores, após adquirir uma licença, os usuários devem inserir suas credenciais para que o servidor possa verificar se os usuários têm uma conta de aluguel.

* **Financiado por anúncios**  - O conteúdo é monetizado pela inclusão da publicidade como parte da experiência. Com esse modelo, o conteúdo pode ser distribuído e não requer autenticação de usuário.

No modo de demonstração do modelo de uso, a lógica de negócios no servidor controla os atributos das licenças geradas. No momento do empacotamento, sua política de DRM só precisa indicar se a autenticação é necessária ou não.

Para habilitar todos os quatro modelos de uso, é necessário incluir apenas duas políticas de DRM:

* Uma política de DRM que permite acesso anônimo ao modelo financiado pelo anúncio
* Uma política DRM que requer autenticação de nome de usuário/senha para os outros três modelos de uso.

Quando um usuário solicita uma licença, um aplicativo cliente pode determinar se deseja solicitar a autenticação do usuário com base nas informações de autenticação nas políticas de DRM.
