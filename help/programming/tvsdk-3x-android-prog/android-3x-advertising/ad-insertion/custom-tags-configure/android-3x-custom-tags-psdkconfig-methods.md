---
description: É possível configurar globalmente nomes de tag personalizados no TVSDK com a classe MediaPlayerItemConfig.
title: Métodos de classe de configuração para tags
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Métodos de classe de configuração para tags {#config-class-methods-for-tags}

É possível configurar globalmente nomes de tag personalizados no TVSDK com a classe MediaPlayerItemConfig.

O TVSDK aplica automaticamente a configuração global a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`MediaPlayerItemConfig` O expõe estes métodos para gerenciar tags personalizadas:

**Assinar tags personalizadas específicas**

| <b>Método</b> | <b>Descrição</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Recupera a lista atual de tags assinadas. |
| `public final void setSubscribedTags(String[] tags);` | Define a lista de tags assinadas que serão expostas ao aplicativo.  Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas pelo `setAdTags`. |

**Personalizar as tags de publicidade usadas pelo detector de oportunidades padrão**

| <b>Método</b> | <b>Descrição</b> |
|--- |--- |
| `public final String[] getAdTags;` | Recupera a lista atual de tags de anúncios. |
| `public final void setAdTags(String[] tags);` | Define a lista de tags de anúncios que serão usadas pelo gerador de oportunidades padrão. |

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro de tags contenha valores nulos.

  Se encontrado, o TVSDK lança um `IllegalArgumentException`.
* O nome da tag personalizada deve conter a `#` prefixo.

  Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.
