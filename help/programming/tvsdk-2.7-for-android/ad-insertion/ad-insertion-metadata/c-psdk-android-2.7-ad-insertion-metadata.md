---
description: Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.
title: Metadados de inserção do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Visão geral {#ad-insertion-metadata-overview}

Para permitir que o resolvedor de anúncios funcione, os provedores de anúncios, como o Adobe Primetime ad decisioning, exigem valores de configuração para habilitar sua conexão com o provedor.

O TVSDK inclui a biblioteca de decisão do anúncio do Primetime. Para que seu conteúdo inclua publicidade do Primetime ad decisioningserver, seu aplicativo deve fornecer as seguintes informações `AuditudeSettings` necessárias:

* `mediaID`, que é um identificador exclusivo para a reprodução do vídeo.

   O editor atribui a mediaID ao enviar o conteúdo de vídeo e as informações do anúncio para o servidor de decisão do anúncio do Adobe Primetime. Essa ID é usada pelo Primetime ad Decisioning para recuperar informações de publicidade relacionadas ao vídeo do servidor.

* (Opcional) `defaultMediaId`, que especifica os anúncios que são veiculados quando as seguintes condições são atendidas:

   * Sua solicitação para o servidor de publicidade é inválida ou o conteúdo está configurado incorretamente.
   * A decisão do anúncio do Primetime está enfrentando atrasos na propagação de dados.
   * Um dos processos de back-end de decisão do Primetime ad está com mau funcionamento ou não está disponível.

   >[!TIP]
   >
   >O Adobe recomenda usar `defaultMediaId`.

* Seu `zoneID`, que é atribuído pelo Adobe, identifica sua empresa ou site.
* O domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

   Você pode incluir esses parâmetros dependendo das suas necessidades e das necessidades do provedor de anúncios.