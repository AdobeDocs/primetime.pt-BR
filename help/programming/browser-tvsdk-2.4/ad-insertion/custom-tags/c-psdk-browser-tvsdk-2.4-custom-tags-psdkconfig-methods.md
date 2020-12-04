---
description: Você pode configurar nomes de tags personalizados em um fluxo com a classe MediaPlayerItemConfig.
seo-description: Você pode configurar nomes de tags personalizados em um fluxo com a classe MediaPlayerItemConfig.
seo-title: Métodos de classe Config para tags
title: Métodos de classe Config para tags
uuid: 222a0349-58d5-4bf3-9d03-e5920610faf5
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Métodos da classe Config para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tags personalizados em um fluxo com a classe MediaPlayerItemConfig.

Para criar um novo `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

Estas são algumas informações sobre como os métodos `MediaPlayerItemConfig` são usados para gerenciar tags personalizadas:

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Assinar tags personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Recupera a lista atual das tags assinadas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Define a lista de tags assinantes expostas ao aplicativo. </p> <p>Seu aplicativo também se inscreve automaticamente em todas as tags transmitidas por meio de <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar as tags de publicidade usadas pelo detector de oportunidade padrão  </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags de anúncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>Define a lista de tags de anúncio a serem usadas pelo gerador de oportunidade padrão. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* O nome da tag personalizada deve conter o prefixo `#`.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.

