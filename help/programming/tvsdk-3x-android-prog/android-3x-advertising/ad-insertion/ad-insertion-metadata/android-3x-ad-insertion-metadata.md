---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.
seo-description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.
seo-title: Metadados de inserção de anúncio
title: Metadados de inserção de anúncio
uuid: 676e81b9-4c2b-487e-bc68-74879ca2966b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Visão geral {#ad-nsertion-metadata-overview}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.

O TVSDK inclui a biblioteca de decisão do anúncio Primetime. Para que seu conteúdo inclua anúncios do servidor de decisão do Primetime ad, seu aplicativo deve fornecer as seguintes informações `AuditudeSettings` necessárias:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncios ao servidor de decisão de publicidade da Adobe Primetime. Essa ID é usada pela decisão do anúncio Primetime para recuperar informações relacionadas ao anúncio do vídeo do servidor.

* (Opcional) `defaultMediaId`, que especifica os anúncios que são veiculados quando as seguintes condições são atendidas:

   * Sua solicitação para o servidor de publicidade é inválida ou o conteúdo está configurado incorretamente.
   * A decisão do Primetime ad está sofrendo atrasos na propagação dos dados.
   * Um dos processos de back-end de decisão do anúncio Primetime está funcionando incorretamente ou indisponível.

   >[!TIP]
   >
   >O Adobe recomenda usar `defaultMediaId`.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

   Você pode incluir esses parâmetros, dependendo de suas necessidades e das necessidades do provedor de publicidade.