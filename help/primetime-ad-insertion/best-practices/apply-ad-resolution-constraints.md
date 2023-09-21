---
title: Aplicar restrições de resolução do anúncio
description: Aplicar restrições de resolução do anúncio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Aplicar restrições de resolução do anúncio {#apply-ad-resolution-constraints}

Pode haver casos em que provedores de anúncios específicos sejam lentos em responder, o que pode fazer com que o tempo de inicialização do vídeo aumente. O Ad Insertion do Primetime suporta tempos limite de solicitações de anúncios e toda a fase de resolução de anúncios para limitar o impacto desses provedores de anúncios lentos.  Anúncios de fallback também podem ser inseridos se os provedores de anúncios de downstream forem muito lentos para responder.  Para obter mais informações, consulte [`ptadtimeout` parâmetro na API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
