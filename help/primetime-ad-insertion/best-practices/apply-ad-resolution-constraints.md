---
title: Aplicar restrições de resolução de anúncio
description: Aplicar restrições de resolução de anúncio
copied-description: true
exl-id: aae17be8-d23c-4c5c-90fd-7ee6fba69e9a
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Aplicar restrições de resolução de anúncio {#apply-ad-resolution-constraints}

Pode haver casos em que provedores de anúncios específicos tenham uma resposta lenta, o que pode fazer com que os tempos de inicialização de vídeo aumentem. O Primetime Ad Insertion suporta tempos limite de solicitações de anúncios e toda a fase de resolução de anúncios para limitar o impacto desses provedores de anúncios lentos.  Anúncios de fallback também podem ser inseridos se os provedores de anúncios downstream estiverem muito lentos para responder.  Para obter mais informações, consulte o parâmetro [`ptadtimeout` na API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
