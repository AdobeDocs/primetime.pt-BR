---
description: Você pode ativar o rastreamento de anúncio do cliente adicionando os parâmetros de versão do modo de rastreamento e do modo de rastreamento à solicitação de URL do Bootstrap.
seo-description: Você pode ativar o rastreamento de anúncio do cliente adicionando os parâmetros de versão do modo de rastreamento e do modo de rastreamento à solicitação de URL do Bootstrap.
seo-title: Ativar o rastreamento de anúncios do cliente
title: Ativar o rastreamento de anúncios do cliente
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 1%

---


# Ativar o rastreamento de anúncios do cliente {#enable-client-side-ad-tracking}

Você pode ativar o rastreamento de anúncios do cliente adicionando os parâmetros `pttrackingmode` e `pttrackingversion` à solicitação de URL do Bootstrap.

Com o rastreamento de anúncio do cliente ativado, você também pode recuperar metadados de rastreamento de anúncio usando o URL da API de rastreamento. Para obter mais detalhes, consulte [Parâmetros de Query](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Para executar o rastreamento de anúncio do cliente, use o URL da API de rastreamento.

1. Adicione os seguintes parâmetros de query ao URL de solicitação do servidor manifest:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Por exemplo:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
