---
title: Configurar o Ad Insertion do Adobe Primetime
description: Configuração do Ad Insertion Adobe Primetime
exl-id: 3720c4b3-08d0-48b8-bb4b-24449e453263
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configurar o Ad Insertion do Adobe Primetime {#ptai-setup}

O processo para configurar o Ad Insertion do Primetime é o seguinte:

1. Integre o servidor de publicidade ao Ad Insertion do Primetime, fazendo logon no console do Ad Insertion do Primetime e configurando as regras de redirecionamento. Para obter mais informações, consulte [Integração do servidor de publicidade](/help/primetime-ad-insertion/getting-started/integrate-ad-server.md).

1. Configure canais ou plataformas no console do Primetime Ad Insertion para garantir dimensões de relatório adequadas.

1. Configure e integre seu CDN ao Primetime Ad Insertion. Para obter mais informações, consulte [Integração da CDN](integrate-cdn.md).

1. Determine se o reempacotamento de anúncios just-in-time é necessário para o fluxo de trabalho do anúncio. Entre em contato com o representante de suporte do Primetime para ativar o serviço.

1. Atualize seu aplicativo para usar o [API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) para fazer e receber solicitações para o Ad Insertion do Primetime e configurar seu aplicativo para oferecer suporte. Para obter mais informações, consulte [Rastreamento de anúncios](set-up-ad-tracking.md).

1. Teste seu aplicativo para garantir a reprodução correta do anúncio usando o [Ferramentas de depuração](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/troubleshoot-and-debug.md).

1. Teste seus aplicativos para garantir o acionamento correto do rastreamento de anúncios e de sinais de impressão usando o [Relatórios](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/reporting-and-billing.md).
