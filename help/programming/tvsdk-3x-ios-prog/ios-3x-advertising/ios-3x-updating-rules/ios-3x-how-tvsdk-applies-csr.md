---
description: nulo
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: nulo
seo-title: Aplicar regras de seleção criativa
title: Aplicar regras de seleção criativa
uuid: 2f009776-201c-418e-aa8f-cb409d0046d8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Aplicar regras de seleção criativa {#apply-creative-selection-rules}

O TVSDK aplica regras de seleção criativa das seguintes maneiras:

* O TVSDK aplica todas as regras `default` primeiro, seguidas pelas regras específicas da zona.
* O TVSDK ignora quaisquer regras que não estejam definidas para a ID de zona atual.
* Depois que o TVSDK aplicar as regras padrão, as regras específicas da zona poderão alterar ainda mais as prioridades criativas com base nas `host` (domínio) correspondências no anúncio selecionado pelas regras `default`.

* No arquivo de regras de amostra incluído com regras de zona adicionais, uma vez que o TVSDK aplique as regras `default`, se o domínio criativo M3U8 não contiver [!DNL my.domain.com] ou [!DNL a.bcd.com] e a zona do anúncio for `1234`, os criativos serão reordenados e o Flash do criativo VPAID será reproduzido primeiro, se disponível. Caso contrário, um anúncio MP4 será reproduzido, e assim por diante, até o JavaScript.

* Se um anúncio for selecionado e o TVSDK não puder ser reproduzido nativamente ( [!DNL .mp4], [!DNL .flv] etc.), o TVSDK emitirá uma solicitação de reempacotamento.

Observe que os tipos de anúncio que podem ser manipulados pelo TVSDK ainda são definidos pela configuração `validMimeTypes` em `AuditudeSettings`.