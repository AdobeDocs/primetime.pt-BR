---
title: Introdução ao Adobe Primetime Ad Insertion
description: Introdução ao Adobe Primetime Ad Insertion
exl-id: 629ea2a5-1b50-4451-a478-95d02f192145
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Introdução ao Adobe Primetime Ad Insertion {#ptai-get-started}

O Primetime Ad Insertion coordena os sistemas que fornecem conteúdo e anúncios para criar experiências de anúncio personalizadas e em fluxo e, em seguida, rastrear a reprodução de anúncios dos anunciantes.

O Primetime Ad Insertion interage com aplicativos clientes de entrega de vídeo reescrevendo manifestos de vídeo para fornecer anúncios direcionados e experiências personalizadas para cada visualizador. Esses manifestos combinam conteúdo e anúncios fornecidos por um servidor de anúncios e podem, opcionalmente, incluir metadados contendo instruções detalhadas de rastreamento de anúncios. O Ad Insertion do Primetime oferece suporte ao rastreamento de anúncios do lado do cliente e do lado do servidor.

Após a configuração correta do sistema, um fluxo de trabalho típico pode ser semelhante ao seguinte:

1. O aplicativo cliente gera um [URL do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) com informações sobre o fluxo de vídeo e envia uma solicitação GET para o Primetime Ad Insertion.  O Primetime Ad Insertion suporta HLS e DASH com uma variedade de formatos de sinalização de anúncios.

1. O Ad Insertion do Primetime responde enviando o manifesto de conteúdo do CDN do editor de volta para o aplicativo cliente.

1. O aplicativo cliente escolhe fluxos apropriados no manifesto gerado para reprodução e faz solicitações ao Ad Insertion do Primetime.

1. O Primetime Ad Insertion busca o(s) fluxo(s) solicitado(s) do CDN de conteúdo, analisa/lê todas as informações de sinalização, faz chamadas para o servidor de publicidade e substitui ad breaks conforme necessário.

1. O Ad Insertion do Primetime normaliza o manifesto reescrevendo URLs de recursos e detectando se os anúncios criados exigem transcodificação, consulte [Transcodificação de anúncios just-in-time](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. O Primetime Ad Insertion busca os anúncios necessários e insere os fragmentos apropriados nos manifestos.

1. O Primetime Ad Insertion fornece os manifestos compilados finais, incluindo anúncios, ao aplicativo cliente para reprodução.

1. A entrega e a visibilidade do anúncio podem ser medidas pelo rastreamento de anúncios do cliente ou do servidor. Consulte [Configuração do rastreamento de anúncios](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

O Primetime Ad Insertion suporta a maioria das configurações de cliente e reprodutor HLS/DASH. Para obter mais informações sobre formatos específicos de sinalização de anúncios suportados, consulte [Formatos de sinalização compatíveis](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
