---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a decisão do Adobe Primetime e do anúncio, exigem valores de configuração para permitir a conexão com o provedor.
seo-description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a decisão do Adobe Primetime e do anúncio, exigem valores de configuração para permitir a conexão com o provedor.
seo-title: Metadados de inserção de anúncio
title: Metadados de inserção de anúncio
uuid: ee4dd8b8-4c41-4f01-be50-60f4c7dc962d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Visão geral {#ad-insertion-metadata-overview}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a decisão do Adobe Primetime e do anúncio, exigem valores de configuração para permitir a conexão com o provedor.

O TVSDK inclui a biblioteca de decisão do anúncio Primetime. Para que seu conteúdo inclua anúncios do servidor de decisão do Primetime ad, seu aplicativo deve fornecer as seguintes `AuditudeSettings` informações necessárias:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncios ao servidor de decisão do Adobe Primetime ad. Essa ID é usada pela decisão do anúncio Primetime para recuperar informações relacionadas ao anúncio do vídeo do servidor.

* (Opcional) `defaultMediaId`, que especifica os anúncios que são veiculados quando as seguintes condições são atendidas:

   * Sua solicitação para o servidor de publicidade é inválida ou o conteúdo está configurado incorretamente.
   * A decisão do Primetime ad está sofrendo atrasos na propagação dos dados.
   * Um dos processos de back-end de decisão do anúncio Primetime está funcionando incorretamente ou indisponível.
   >[!TIP]
   >
   >A Adobe recomenda usar `defaultMediaId`.

* Sua empresa `zoneID`, que é atribuída pela Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

   Você pode incluir esses parâmetros, dependendo de suas necessidades e das necessidades do provedor de publicidade.