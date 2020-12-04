---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.
seo-description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.
seo-title: Metadados de inserção de anúncio
title: Metadados de inserção de anúncio
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Visão geral {#ad-insertion-metadata-overview}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como a tomada de decisões de anúncios da Adobe Primetime, exigem valores de configuração para permitir a conexão com o provedor.

O TVSDK do navegador inclui a biblioteca de decisão de anúncio do Adobe Primetime. Para que seu conteúdo inclua anúncios do servidor de decisão de publicidade da Adobe Primetime, seu aplicativo deve fornecer as seguintes informações obrigatórias de AudidtudeSettings:

* `mediaID`, que é um identificador exclusivo para o vídeo a ser reproduzido.

   O editor atribui a mediaID ao enviar conteúdo de vídeo e informações de anúncios ao servidor de decisão de publicidade da Adobe Primetime. Essa ID é usada pela decisão de publicidade da Adobe Primetime para recuperar informações relacionadas ao vídeo do servidor.

* (Opcional) `defaultMediaId`, que especifica os anúncios que são veiculados quando as seguintes condições são atendidas:

   * Sua solicitação para o servidor de publicidade é inválida ou o conteúdo está configurado incorretamente.
   * A tomada de decisões de anúncios da Adobe Primetime está sofrendo atrasos na propagação dos dados.
   * Um dos processos back-end de decisão de anúncio da Adobe Primetime está funcionando incorretamente ou indisponível.

   >[!TIP]
   >
   >O Adobe recomenda usar `defaultMediaId`.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

   Você pode incluir esses parâmetros, dependendo de suas necessidades e das necessidades do provedor de publicidade.