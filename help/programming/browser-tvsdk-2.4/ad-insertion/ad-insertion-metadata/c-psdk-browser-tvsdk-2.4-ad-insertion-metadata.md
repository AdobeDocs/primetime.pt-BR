---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.
title: Adicionar metadados de inserção
exl-id: 8d6cb371-8666-4b55-b828-0f1d495e7fb7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Visão geral {#ad-insertion-metadata-overview}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.

O TVSDK do navegador inclui a biblioteca de decisões de anúncios do Adobe Primetime. Para que o conteúdo inclua anúncios do servidor do Adobe Primetime ad decisioning, o aplicativo deve fornecer as seguintes informações necessárias do AudidtudeSettings:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncio para o servidor do Adobe Primetime Ad Decisioning. Essa ID é usada pela Adobe Primetime Ad Decisioning para recuperar informações de publicidade relacionadas ao vídeo do servidor.

* (Opcional) `defaultMediaId`, que especifica os anúncios veiculados quando as seguintes condições são atendidas:

   * Sua solicitação ao servidor de publicidade é inválida ou o conteúdo está configurado incorretamente.
   * O Adobe Primetime ad decisioning está enfrentando atrasos na propagação dos dados.
   * Um dos processos de back-end do Adobe Primetime Ad Decisioning está com defeito ou indisponível.

   >[!TIP]
   >
   >O Adobe recomenda usar `defaultMediaId`.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de direcionamento.

   Você pode incluir esses parâmetros dependendo das suas necessidades e das necessidades do provedor de anúncios.
