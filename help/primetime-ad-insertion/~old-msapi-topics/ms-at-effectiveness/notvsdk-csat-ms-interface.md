---
description: Use os parâmetros de consulta opcionais pttrackingmode, pttrackingversion e pttrackingposition para obter URLs para os quais enviar informações de rastreamento de anúncio sobre o vídeo atual. As respostas variam com a versão de rastreamento e se o fluxo de vídeo está ao vivo ou sob demanda (VOD).
title: API para os reprodutores interagirem com o servidor de manifesto
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# API para os reprodutores interagirem com o servidor de manifesto {#api-for-players-to-interact-with-the-manifest-server}

Use o opcional `pttrackingmode`, `pttrackingversion`, e `pttrackingposition` consulte parâmetros para obter URLs para os quais enviar informações de rastreamento de anúncios sobre o vídeo atual. As respostas variam com a versão de rastreamento e se o fluxo de vídeo está ao vivo ou sob demanda (VOD).

## Parâmetros de consulta {#query-parameters}

**pttrackingmode**

Exemplo: `pttrackingmode=simple`
Especificar simples informa ao servidor de manifesto que você deseja rastrear as informações.
Especifique em uma solicitação para buscar o M3U8 antes de solicitar informações de rastreamento. Quando você não o especifica, o servidor de manifesto retorna informações de rastreamento nas tags #EXT-X-MARKER.
Ou, se você especificar um valor válido diferente de simples, o rastreamento do lado do servidor será chamado.

**pttrackingversion**

Exemplo: `pttrackingversion=v2`
Esse parâmetro informa ao servidor de manifesto qual formato usar para retornar as informações de rastreamento (consulte [Formatos de arquivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Especifique em uma solicitação para buscar o M3U8 antes de solicitar informações de rastreamento. Quando você não o especifica ou especifica um valor inválido, o servidor de manifesto usa v1.

**pttrackingposition**

Exemplo: `pttrackingposition`
Esse parâmetro informa ao servidor de manifesto para retornar informações de rastreamento do vídeo como um objeto JSON ou VMAP no arquivo M3U8. O servidor de manifesto ignora o valor especificado e envia todas as informações de rastreamento que ele tem para essa sessão. Se nenhum valor for transmitido, o servidor de manifesto retornará o arquivo M3U8 solicitado.
