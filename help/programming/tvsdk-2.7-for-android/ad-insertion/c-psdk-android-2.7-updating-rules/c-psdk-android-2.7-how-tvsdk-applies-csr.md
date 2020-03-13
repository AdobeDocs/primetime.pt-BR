---
description: nulo
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: nulo
seo-title: Aplicar regras de seleção criativa
title: Aplicar regras de seleção criativa
uuid: 75109483-ea60-43a8-92e7-4bcba48986bc
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Aplicar regras de seleção criativa {#apply-creative-selection-rules}

O TVSDK aplica regras de seleção criativa das seguintes maneiras:

* O TVSDK aplica todas as `default` regras primeiro, seguido pelas regras específicas da zona.
* O TVSDK ignora quaisquer regras que não estejam definidas para a ID de zona atual.
* Depois que o TVSDK aplicar as regras padrão, as regras específicas da zona poderão alterar ainda mais as prioridades criativas com base nas correspondências `host` (domínio) no anúncio selecionado pelas `default` regras.

* No arquivo de regras de amostra incluído com regras de zona adicionais, uma vez que o TVSDK aplique as `default` regras, se o domínio criativo do M3U8 não contiver [!DNL my.domain.com] ou [!DNL a.bcd.com] e a zona do anúncio for `1234`, os criativos serão reorganizados e o anúncio do Flash VPAID será reproduzido primeiro, se disponível. Caso contrário, um anúncio MP4 será reproduzido, e assim por diante, até o JavaScript.

* Se um anúncio for selecionado e o TVSDK não puder ser reproduzido nativamente ( [!DNL .mp4], [!DNL .flv], etc.), o TVSDK emitirá uma solicitação de reempacotamento.

Observe que os tipos de anúncio que podem ser manipulados pelo TVSDK ainda são definidos pela `validMimeTypes` configuração em `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

