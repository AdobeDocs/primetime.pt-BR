---
keywords: regras de seleção criativa;AdobeTVSDKConfig
title: Aplicar regras de seleção criativa
description: Aplicar regras de seleção criativa
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Aplicar regras de seleção criativa {#apply-creative-selection-rules}

O TVSDK aplica regras de seleção criativa das seguintes maneiras:

* O TVSDK aplica todas as regras `default` primeiro, seguidas pelas regras específicas da zona.
* O TVSDK ignora quaisquer regras que não estejam definidas para a ID de zona atual.
* Quando o TVSDK aplica as regras padrão, as regras específicas da zona podem alterar ainda mais as prioridades criativas com base nas `host` (domínio) correspondências no anúncio selecionado pelas regras `default`.

* No arquivo de regras de amostra incluído com regras de zona adicionais, uma vez que o TVSDK aplique as regras `default`, se o domínio criativo M3U8 não contiver `my.domain.com` ou `a.bcd.com` e a zona de anúncio for `1234`, os anúncios serão reordenados e o anúncio VPAID do Flash será reproduzido primeiro, se disponível. Caso contrário, um anúncio MP4 será reproduzido, e assim por diante, para JavaScript.

* Se um anúncio criativo for selecionado e o TVSDK não puder ser reproduzido nativamente ( [!DNL .mp4], [!DNL .flv], etc.), o TVSDK emitirá uma solicitação de reempacotamento.

Observe que os tipos de anúncios que podem ser manipulados pelo TVSDK ainda são definidos por meio da configuração `validMimeTypes` em `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

