---
description: A implementação de referência ilustra como configurar o player para anúncios, o que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução de anúncios anteriores, intermediários e posteriores em fluxos de vídeo VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.
seo-description: A implementação de referência ilustra como configurar o player para anúncios, o que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução de anúncios anteriores, intermediários e posteriores em fluxos de vídeo VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.
seo-title: Inserção de anúncio
title: Inserção de anúncio
uuid: 75c1d77a-a7ff-4cb6-ad7f-7c83a950b7cb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Inserção de anúncio {#ad-insertion}

A implementação de referência ilustra como configurar o player para anúncios, o que inclui a configuração de metadados de vídeo para inserção de anúncios e a resolução de anúncios anteriores, intermediários e posteriores em fluxos de vídeo VOD ou ao vivo/linear. Também ilustra como lidar com anúncios clicáveis.

O processo de configuração de um player para inserção de anúncios inclui:

* **Feed de entrada:** Preenchimento de um feed de entrada com metadados de anúncio. Consulte [Formato de catálogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adaptador de feed de implementação de referência:** Analisando o feed de entrada para preencher um objeto de metadados de anúncio.
* **AdsManager:** usar o AdsManager para recuperar os metadados do anúncio e criar o AdProvider correspondente.