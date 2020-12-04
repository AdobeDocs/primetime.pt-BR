---
description: Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig.
seo-description: Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig.
seo-title: Métodos de classe Config para tags
title: Métodos de classe Config para tags
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Métodos da classe Config para tags {#config-class-methods-for-tags}

Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig.

O TVSDK aplica automaticamente a configuração global a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`MediaPlayerItemConfig` expõe esses métodos para gerenciar as tags personalizadas:

**Assinar tags personalizadas específicas**

| <b>Método</b> | <b>Descrição</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Recupera a lista atual das tags assinadas. |
| `public final void setSubscribedTags(String[] tags);` | Define a lista de tags assinadas que serão expostas ao aplicativo.  Seu aplicativo também se inscreve automaticamente em todas as tags transmitidas por meio de `setAdTags`. |

**Personalizar as tags de publicidade usadas pelo detector de oportunidade padrão**

| <b>Método</b> | <b>Descrição</b> |
|--- |--- |
| `public final String[] getAdTags;` | Recupera a lista atual de tags de anúncio. |
| `public final void setAdTags(String[] tags);` | Define a lista de tags de anúncio que serão usadas pelo gerador de oportunidade padrão. |

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro tags contenha valores nulos.

   Se encontrado, o TVSDK lança um `IllegalArgumentException`.
* O nome da tag personalizada deve conter o prefixo `#`.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.