---
description: A implementação de referência ilustra como configurar o reprodutor para anúncios, que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução dos anúncios antes, depois e depois da exibição em fluxos de vídeo VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.
title: Inserção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Inserção de anúncio {#ad-insertion}

A implementação de referência ilustra como configurar o reprodutor para anúncios, que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução dos anúncios antes, depois e depois da exibição em fluxos de vídeo VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.

O processo de configuração de um reprodutor para inserção de anúncio inclui:

* **Feed de entrada:** preenchimento de um feed de entrada com metadados de anúncio. Consulte [Formato do catálogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adaptador de feed de implementação de referência:**  analisar o feed de entrada para preencher um objeto de metadados de anúncio.
* **AdsManager:** utilizando o AdsManager para recuperar os metadados do anúncio e criar o AdProvider correspondente.