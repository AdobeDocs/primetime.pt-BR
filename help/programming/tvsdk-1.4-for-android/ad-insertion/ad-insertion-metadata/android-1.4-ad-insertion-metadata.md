---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.
title: Adicionar metadados de inserção
exl-id: 7245b42c-f3ba-43ec-b895-c1a2d66aa11f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Visão geral {#ad-insertion-metadata}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.

O TVSDK inclui a biblioteca de decisão de anúncios do Primetime. Para que seu conteúdo inclua anúncios do servidor do Primetime ad decisioning, seu aplicativo deve fornecer os seguintes itens necessários `AuditudeSettings` informações:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a `mediaID` ao enviar conteúdo de vídeo e informações de anúncios para o servidor do Adobe Primetime ad decisioning. Essa ID é usada pela decisão de anúncio do Primetime para recuperar informações de anúncio relacionadas ao vídeo do servidor.

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
