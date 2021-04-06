---
title: Solução de problemas e depurar
description: Solução de problemas e depurar
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Solução de problemas e depurar {#troubleshooting-debugging}

O Primetime Ad Insertion oferece ferramentas para identificar e diagnosticar problemas que podem ocorrer em todas as fases da entrega de vídeo, como erros de entrega de CDN, erros criativos de anúncio ou erros de conectividade de cliente.

O Primetime Ad Insertion suporta registro detalhado por meio do [parâmetro da API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` ou `ptdebug=AdCall` para o URL de inicialização. Os logs são emitidos para cabeçalhos de resposta HTTP e para o console do Primetime Ad Insertion. Esse parâmetro destina-se somente a testes localizados, não para fluxos de produção. Para obter mais informações sobre tipos de mensagem quando o registro em log detalhado está ativado, consulte [ptdebug registrando eventos em log detalhado](verbose-logging.md#ptdebug-logging-events).

O Primetime Ad Insertion também fornece a depuração de desempenho em todas as solicitações com o cabeçalho X-ADBE-AI-X1, que pode ser usado para medir o desempenho e as inserções de anúncios em qualquer solicitação específica. Esse cabeçalho de solicitação está disponível independentemente de o registro detalhado estar habilitado. Para obter mais informações, consulte [Cabeçalhos detalhados: X-ADBE-PTAI-X1](debugging-headers.md).
