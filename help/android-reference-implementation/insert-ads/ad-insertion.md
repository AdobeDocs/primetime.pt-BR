---
description: A implementação de referência ilustra como configurar o reprodutor para anúncios, o que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução de anúncios precedentes, intermediários e posteriores em fluxos de vídeo de VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.
title: Inserção de anúncio
exl-id: 3c2d8fca-2a0e-4577-81f3-7b390f6396e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Inserção de anúncio {#ad-insertion}

A implementação de referência ilustra como configurar o reprodutor para anúncios, o que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução de anúncios precedentes, intermediários e posteriores em fluxos de vídeo de VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.

O processo de configuração de um reprodutor para inserção de anúncio inclui:

* **Feed de entrada:** Preencher um feed de entrada com metadados de anúncio. Consulte [Formato do catálogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adaptador de feed de implementação de referência:** Analisar o feed de entrada para preencher um objeto de metadados de anúncio.
* **AdsManager:** Usar o AdsManager para recuperar os metadados do anúncio e criar o AdProvider correspondente.
