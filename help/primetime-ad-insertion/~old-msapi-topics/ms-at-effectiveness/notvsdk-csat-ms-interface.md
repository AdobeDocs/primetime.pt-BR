---
description: Use os parâmetros opcionais de query pttrackingmode, pttrackingversion e pttrackingposition para obter URLs para os quais enviar informações de rastreamento de anúncio sobre o vídeo atual. As respostas variam com a versão de rastreamento e se o fluxo de vídeo é ao vivo ou sob demanda (VOD).
seo-description: Use os parâmetros opcionais de query pttrackingmode, pttrackingversion e pttrackingposition para obter URLs para os quais enviar informações de rastreamento de anúncio sobre o vídeo atual. As respostas variam com a versão de rastreamento e se o fluxo de vídeo é ao vivo ou sob demanda (VOD).
seo-title: API para que os players interajam com o servidor manifest
title: API para que os players interajam com o servidor manifest
uuid: ab7a19e7-6c28-4960-a56b-3b33c525e6b3
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# API para que os players interajam com o servidor de manifesto {#api-for-players-to-interact-with-the-manifest-server}

Use os parâmetros opcionais de query `pttrackingmode`, `pttrackingversion` e `pttrackingposition` para obter URLs para os quais enviar informações de rastreamento de anúncio sobre o vídeo atual. As respostas variam com a versão de rastreamento e se o fluxo de vídeo é ao vivo ou sob demanda (VOD).

## Parâmetros de query {#query-parameters}

**modo de rastreamento**

Exemplo: `pttrackingmode=simple`
A especificação simples informa ao servidor manifest que você deseja rastrear as informações.
Especifique-o em uma solicitação para buscar o M3U8 antes de solicitar informações de rastreamento.Quando você não as especifica, o servidor manifest retorna informações de rastreamento nas tags #EXT-X-MARKER.
Ou, se você especificar um valor válido diferente de simples, o rastreamento do lado do servidor será chamado.

**pttrackingversion**

Exemplo: `pttrackingversion=v2`
Este parâmetro informa ao servidor manifest qual formato usar para retornar informações de rastreamento (consulte [Formatos de arquivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Especifique-o em uma solicitação para buscar o M3U8 antes de solicitar informações de rastreamento.Quando você não as especifica ou especifica um valor inválido, o servidor manifest usa v1.

**posição**

Exemplo: `pttrackingposition`
Este parâmetro diz ao servidor manifest para retornar as informações de rastreamento do vídeo como um objeto JSON ou VMAP no arquivo M3U8. O servidor manifest ignora o valor especificado e envia todas as informações de rastreamento que tem para essa sessão. Se nenhum valor for transmitido, o servidor manifest retornará o arquivo M3U8 solicitado.
