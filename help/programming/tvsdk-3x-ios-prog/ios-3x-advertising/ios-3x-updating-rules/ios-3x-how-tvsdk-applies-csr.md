---
keywords: regras de seleção criativa;AdobeTVSDKConfig
title: Aplicar regras de seleção criativa
description: Aplicar regras de seleção criativa
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Aplicar regras de seleção criativa {#apply-creative-selection-rules}

O TVSDK aplica regras de seleção criativa das seguintes maneiras:

* O TVSDK aplica tudo `default` primeiro, seguido pelas regras específicas da região.
* O TVSDK ignora todas as regras que não estão definidas para a ID de zona atual.
* Depois que o TVSDK aplica as regras padrão, as regras específicas da região podem alterar ainda mais as prioridades criativas com base no `host` (domínio) corresponde no criativo selecionado pelo `default` regras.

* No arquivo de regras de exemplo incluído com regras de zona adicionais, depois que o TVSDK aplica a variável `default` regras, se o domínio criativo M3U8 não contiver [!DNL my.domain.com] ou [!DNL a.bcd.com] e a zona de publicidade é `1234`, os componentes criativos são reordenados e o criativo VPAID do Flash é reproduzido primeiro, se disponível. Caso contrário, um anúncio MP4 será reproduzido e assim por diante, até o JavaScript.

* Se um criativo de anúncio for selecionado, o TVSDK não poderá ser reproduzido nativamente ( [!DNL .mp4], [!DNL .flv], etc.), o TVSDK emite uma solicitação de reempacotamento.

Observe que os tipos de anúncios que podem ser manipulados pelo TVSDK ainda são definidos por meio do `validMimeTypes` configuração em `AuditudeSettings`.
