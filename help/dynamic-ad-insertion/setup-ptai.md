---
title: Configurar o Adobe Primetime Ad Insertion
description: Configuração do Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Configurar o Adobe Primetime Ad Insertion {#ptai-setup}

O processo para configurar o Primetime Ad Insertion é o seguinte:

1. Integre seu servidor de publicidade ao Primetime Ad Insertion fazendo logon no console do Primetime Ad Insertion e configurando regras de redirecionamento. Para obter mais informações, consulte [Integração do servidor](integrate-ad-server.md)de anúncios.

1. Configure canais ou plataformas no console Ad Insertion Primetime para garantir dimensões de relatórios adequadas.

1. Configure e integre seu CDN no Primetime Ad Insertion. Para obter mais informações, consulte [Integração do CDN](integrate-cdn.md).

1. Determine se o reempacotamento de anúncio em tempo real é necessário para o fluxo de trabalho do anúncio. Entre em contato com o representante de suporte do Primetime para habilitar o serviço.

1. Atualize seu aplicativo para usar a API [do](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) Bootstrap para fazer e receber solicitações do Primetime Ad Insertion e configure seu aplicativo para suportar. Para obter mais informações, consulte Rastreamento de [anúncios](set-up-ad-tracking.md).

1. Teste seu aplicativo para garantir a reprodução correta do anúncio. <!-- using the [Debugging tools](troubleshoot-and-debug.md).-->

1. Teste seus aplicativos para garantir o acionamento correto do rastreamento de anúncios e sinais de impressão.<!-- using the [Reporting](reporting-and-billing.md).-->
