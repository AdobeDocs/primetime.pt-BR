---
description: Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe PTSDKConfig.
seo-description: Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe PTSDKConfig.
seo-title: Métodos de classe Config para tags
title: Métodos de classe Config para tags
uuid: 1d3651a0-3b70-4d3a-8ced-663a9dad7205
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Métodos de classe Config para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe PTSDKConfig.

O TVSDK aplica a configuração global automaticamente a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`PTSDKConfig` expõe esses métodos para gerenciar as tags personalizadas:

| **Assinar tags personalizadas específicas** |
|---|
| `subscribedTags` | Recupera a lista atual de tags assinadas. |
| `setSubscribedTags` | Define a lista de tags assinadas que serão expostas ao aplicativo. |
| **Personalizar as tags de publicidade usadas pelo detector de oportunidade padrão** |
| `adTags` | Recupera a lista atual de tags de publicidade. |
| `setAdTags` | Define a lista de tags de publicidade que serão usadas pelo gerador de oportunidade padrão. |

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro tags contenha valores nulos.
* O nome da tag personalizada deve conter o prefixo #.

   Por exemplo, #EXT-X-ASSET é um nome de tag personalizado correto, mas EXT-X-ASSET está incorreto.
* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.

