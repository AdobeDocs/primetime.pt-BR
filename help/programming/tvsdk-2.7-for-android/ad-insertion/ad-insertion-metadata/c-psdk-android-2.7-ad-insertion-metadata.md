---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.
title: Adicionar metadados de inserção
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Visão geral {#ad-insertion-metadata-overview}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.

O TVSDK inclui a biblioteca de decisão de anúncios do Primetime. Para que o conteúdo inclua anúncios do servidor do Primetime ad decisioning, o aplicativo deve fornecer os seguintes itens necessários `AuditudeSettings` informações:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

  O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncio para o servidor do Adobe Primetime Ad Decisioning. Essa ID é usada pela decisão de anúncio do Primetime para recuperar informações de anúncio relacionadas ao vídeo do servidor.

* (Opcional) `defaultMediaId`, que especifica os anúncios veiculados quando as seguintes condições são atendidas:

   * Sua solicitação ao servidor de publicidade é inválida ou o conteúdo está configurado incorretamente.
   * O Primetime e a decisão estão enfrentando atrasos na propagação dos dados.
   * Um dos processos de back-end do Primetime e do Decisioning está com defeito ou indisponível.

  >[!TIP]
  >
  >O Adobe recomenda usar `defaultMediaId`.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de direcionamento.

  Você pode incluir esses parâmetros dependendo das suas necessidades e das necessidades do provedor de anúncios.
