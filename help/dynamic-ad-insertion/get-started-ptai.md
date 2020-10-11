---
title: Introdução ao Adobe Primetime Ad Insertion
description: Introdução ao Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Introdução ao Adobe Primetime Ad Insertion {#ptai-get-started}

O Primetime Ad Insertion coordena os sistemas que fornecem conteúdo e anúncios para criar experiências de anúncios personalizadas e em fluxo e, em seguida, rastrear a reprodução de anúncios para seus anunciantes.

O Primetime Ad Insertion interage com os aplicativos clientes de delivery de vídeo, regravando os manifestos de vídeo para fornecer anúncios direcionados e experiências personalizadas para cada visualizador.Esses manifestos combinam o conteúdo e os anúncios fornecidos de um servidor de anúncios e podem, opcionalmente, incluir metadados que contêm instruções detalhadas de rastreamento de anúncios. O Primetime Ad Insertion suporta o rastreamento de anúncios do lado do cliente e do lado do servidor.

Após a configuração correta do sistema, um fluxo de trabalho típico pode ser exibido da seguinte maneira:

1. O aplicativo cliente gera um URL [de](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) Bootstrap com informações sobre o fluxo de vídeo e envia uma solicitação de GET para o Primetime Ad Insertion.

1. O Primetime Ad Insertion responde enviando o manifesto de conteúdo do CDN do editor para o aplicativo cliente.

1. O aplicativo cliente escolhe fluxos apropriados no manifesto gerado para reproduzir e faz solicitações ao Primetime Ad Insertion.

1. O Primetime Ad Insertion busca os fluxos solicitados do CDN de conteúdo, analisa/lê quaisquer informações de dicas, efetua chamadas para o servidor de anúncios e substitui as quebras de anúncios, conforme necessário.

1. O Primetime Ad Insertion normaliza o manifesto, regravando os URLs de recursos e detectando se os anúncios exigem transcodificação, consulte [just-in-time ad transcoding](just-in-time-transcoding.md) and [package](just-in-time-repackaging.md).

1. O Primetime Ad Insertion busca os anúncios necessários e insere os fragmentos apropriados nos manifestos.

1. O Primetime Ad Insertion fornece os manifestos finais marcados, incluindo anúncios, ao aplicativo cliente para reprodução.

1. O delivery e a capacidade de visualização do anúncio podem ser medidos através do rastreamento de anúncios do cliente ou do servidor, consulte [Configuração do rastreamento](set-up-ad-tracking.md)de anúncios.

O Primetime Ad Insertion suporta a maioria das configurações de cliente para HLS/DASH.
