---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Visão geral{#overview}

A Implementação de referência inclui uma opção de modo de demonstração que demonstra como implementar diferentes modelos de uso para um segmento de conteúdo empacotado. O modo de demonstração apresenta uma lógica comercial para estes modelos de uso:

* **Download por conta própria (DTO)** - Os usuários podem baixar o conteúdo online ou offline e recebem uma licença permanente para o conteúdo.
* **Aluguel/vídeo sob demanda (VOD)** - O conteúdo disponível vem com restrições baseadas em tempo. Por exemplo, os usuários podem reproduzir conteúdo durante um período de 30 dias. Depois que a reprodução começar, o usuário terá até 48 horas para terminar de assistir ao conteúdo. O conteúdo deve ser visualizado em 30 dias.
* **Assinatura (tudo o que você pode comer)** - Alguns serviços oferecem assinaturas pagas que dão aos usuários acesso ilimitado a uma grande biblioteca de conteúdo, desde que continuem pagando uma taxa mensal. O servidor de licenças emite uma licença exclusiva para cada segmento de conteúdo e também emite uma licença raiz que expira no final do período de assinatura. Todos os meses, quando os usuários renovam suas assinaturas, a licença raiz também deve ser renovada.

  >[!NOTE]
  >
  >Para os modelos de uso anteriores, após adquirir uma licença, os usuários devem inserir suas credenciais para que o servidor possa verificar se os usuários têm uma conta de aluguel.

* **Financiado por anúncio** - O conteúdo é monetizado ao incluir publicidade como parte da experiência. Com esse modelo, o conteúdo pode ser distribuído e não requer autenticação do usuário.

No modo de demonstração de modelo de uso, a lógica comercial no servidor controla os atributos para licenças geradas. No momento do empacotamento, a política de DRM só precisa indicar se a autenticação é necessária.

Para habilitar todos os quatro modelos de uso, você só precisa incluir duas políticas DRM:

* Uma política DRM que permite acesso anônimo ao modelo financiado por anúncio
* Uma política DRM que requer autenticação de nome de usuário/senha para os outros três modelos de uso.

Quando um usuário solicita uma licença, um aplicativo cliente pode determinar se deve solicitar autenticação ao usuário com base nas informações de autenticação nas políticas do DRM.
