---
title: Aplicar restrições de resolução de anúncios
description: null
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# Aplicar restrições de resolução de anúncios {#apply-ad-resolution-constraints}

Pode haver casos em que provedores de anúncios específicos demoram para responder, o que pode fazer com que o tempo de start do vídeo aumente. O Primetime Ad Insertion suporta tempos limite de solicitações de anúncios e toda a fase de resolução de anúncios para limitar o impacto desses fornecedores de anúncios lentos.  Anúncios de fallback também podem ser inseridos se os provedores de anúncios downstream estiverem muito lentos para responder.  Para obter mais informações, consulte o parâmetro [`ptadtimeout` na API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
