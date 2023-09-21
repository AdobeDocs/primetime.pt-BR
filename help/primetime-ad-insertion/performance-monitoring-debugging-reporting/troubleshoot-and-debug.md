---
title: Solução de problemas e depuração
description: Solução de problemas e depuração
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Solução de problemas e depuração {#troubleshooting-debugging}

O Primetime Ad Insertion oferece ferramentas para identificar e diagnosticar problemas que podem ocorrer em todas as fases da entrega de vídeo, como erros de entrega de CDN, erros de criação de anúncios ou erros de conectividade do cliente.

O Ad Insertion do Primetime suporta registro detalhado via [Parâmetro da API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` ou `ptdebug=AdCall` ao URL de inicialização. Os logs são enviados para os cabeçalhos de resposta HTTP e para o console Ad Insertion do Primetime. Esse parâmetro destina-se somente a testes localizados, não a fluxos de produção. Para obter mais informações sobre tipos de mensagem quando o registro detalhado está ativado, consulte [eventos de log ptdebug no log detalhado](verbose-logging.md#ptdebug-logging-events).

O Ad Insertion do Primetime também fornece depuração de desempenho em todas as solicitações com o cabeçalho X-ADBE-AI-X1, que pode ser usado para medir o desempenho e as inserções de anúncios em qualquer solicitação específica. Esse cabeçalho de solicitação está disponível independentemente de o log detalhado estar ativado ou não. Para obter mais informações, consulte [Cabeçalhos detalhados: X-ADBE-PTAI-X1](debugging-headers.md).
