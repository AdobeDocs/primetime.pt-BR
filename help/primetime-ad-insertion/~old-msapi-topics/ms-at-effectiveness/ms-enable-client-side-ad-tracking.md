---
description: Você pode ativar o rastreamento de anúncios do lado do cliente adicionando os parâmetros de versão pttrackingmode e pttracking à solicitação de URL do Bootstrap.
title: Ativar o rastreamento de anúncios do lado do cliente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 2%

---


# Ativar o rastreamento de anúncios do lado do cliente {#enable-client-side-ad-tracking}

Você pode ativar o rastreamento de anúncios do lado do cliente adicionando os parâmetros `pttrackingmode` e `pttrackingversion` à solicitação de URL do Bootstrap.

Com o rastreamento de anúncios do lado do cliente ativado, você também pode recuperar metadados de rastreamento de anúncios usando o URL da API de rastreamento. Para obter mais detalhes, consulte [Parâmetros de consulta](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Para executar o rastreamento de anúncios do lado do cliente, use o URL da API de rastreamento.

1. Adicione os seguintes parâmetros de consulta ao URL de solicitação do servidor de manifesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Por exemplo:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
