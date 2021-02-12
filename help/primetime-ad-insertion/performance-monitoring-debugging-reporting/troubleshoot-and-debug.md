---
title: Solução de problemas e depuração
description: null
translation-type: tm+mt
source-git-commit: 242b5a2875ebc0e0020296ce9489dd54438b5ad0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Solucionar problemas e depurar {#troubleshooting-debugging}

O Primetime Ad Insertion oferta ferramentas para identificar e diagnosticar problemas que podem ocorrer em todas as fases do delivery de vídeo, como erros de delivery CDN, erros criativos ou erros de conectividade do cliente.

O Primetime Ad Insertion oferece suporte ao logon detalhado pelo [parâmetro da API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` ou `ptdebug=AdCall` para o URL de inicialização. Os registros são enviados para os cabeçalhos de resposta HTTP e para o console do Primetime Ad Insertion. Este parâmetro destina-se apenas a testes localizados, não a fluxos de produção. Para obter mais informações sobre tipos de mensagens quando o registro em log detalhado estiver ativado, consulte [eventos de registro em log detalhado](verbose-logging.md#ptdebug-logging-events).

O Primetime Ad Insertion também fornece depuração de desempenho em todas as solicitações com o cabeçalho X-ADBE-AI-X1, que pode ser usado para medir o desempenho e as inserções de anúncios em qualquer solicitação específica. Esse cabeçalho de solicitação está disponível independentemente de o registro em log detalhado estar habilitado. Para obter mais informações, consulte [Cabeçalhos detalhados: X-ADBE-PTAI-X1](debugging-headers.md).
