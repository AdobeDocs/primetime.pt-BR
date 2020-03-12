---
description: nulo
seo-description: nulo
seo-title: Aplicação de regras de seleção criativas
title: Aplicação de regras de seleção criativas
uuid: 464c32db-1c96-4d91-97ce-f1d95e57c062
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Aplicação de regras de seleção criativas{#applying-creative-selection-rules}

O TVSDK aplica regras de seleção criativa das seguintes maneiras:

* O TVSDK aplica todas as `default` regras primeiro, seguido pelas regras específicas da zona.
* O TVSDK ignora quaisquer regras que não estejam definidas para a ID de zona atual.
* Depois que o TVSDK aplicar as regras padrão, as regras específicas da zona poderão alterar ainda mais as prioridades criativas com base nas correspondências `host` (domínio) no anúncio selecionado pelas `default` regras.

* No arquivo de regras de amostra incluído com regras de zona adicionais, uma vez que o TVSDK aplique as `default` regras, se o domínio criativo do M3U8 não contiver [!DNL my.domain.com] ou [!DNL a.bcd.com] e a zona do anúncio for `1234`, os criativos serão reorganizados e o anúncio do Flash VPAID será reproduzido primeiro, se disponível. Caso contrário, um anúncio MP4 será reproduzido, e assim por diante, até o JavaScript.

* Se um anúncio for selecionado e o TVSDK não puder ser reproduzido nativamente ( [!DNL .mp4], [!DNL .flv], etc.), o TVSDK emitirá uma solicitação de reempacotamento.

Observe que os tipos de anúncio que podem ser manipulados pelo TVSDK ainda são definidos pela `validMimeTypes` configuração em `AuditudeSettings`.
