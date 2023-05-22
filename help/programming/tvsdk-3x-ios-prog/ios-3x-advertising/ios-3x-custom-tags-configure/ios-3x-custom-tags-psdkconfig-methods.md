---
description: Você pode configurar nomes de tag personalizados no TVSDK globalmente com a classe PTSDKConfig.
title: Métodos de classe de configuração para tags
exl-id: 017b766e-a6aa-4c14-af9a-2c88746e22c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Métodos de classe de configuração para tags {#config-class-methods-for-tags}

Você pode configurar nomes de tag personalizados no TVSDK globalmente com a classe PTSDKConfig.

O TVSDK aplica a configuração global automaticamente a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`PTSDKConfig` O expõe estes métodos para gerenciar tags personalizadas:

| **Assinar tags personalizadas específicas** |  |
|---|---|
| `subscribedTags` | Recupera a lista atual de tags assinadas. |
| `setSubscribedTags` | Define a lista de tags assinadas que serão expostas ao aplicativo. |
| **Personalizar as tags de publicidade usadas pelo detector de oportunidades padrão** |
| `adTags` | Recupera a lista atual de tags de anúncios. |
| `setAdTags` | Define a lista de tags de anúncios que serão usadas pelo gerador de oportunidades padrão. |


Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro de tags contenha valores nulos.
* O nome da tag personalizada deve conter o prefixo #.

   Por exemplo, #EXT-X-ASSET é um nome de tag personalizado correto, mas EXT-X-ASSET está incorreto.
* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.
