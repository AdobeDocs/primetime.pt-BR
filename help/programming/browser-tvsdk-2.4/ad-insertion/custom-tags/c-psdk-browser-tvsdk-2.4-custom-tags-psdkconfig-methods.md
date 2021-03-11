---
description: Você pode configurar nomes de tags personalizados em um fluxo com a classe MediaPlayerItemConfig .
title: Métodos da classe Config para tags
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Métodos de classe de configuração para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tags personalizados em um fluxo com a classe MediaPlayerItemConfig .

Para criar um novo `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

Estas são algumas informações sobre como os métodos `MediaPlayerItemConfig` são usados para gerenciar tags personalizadas:

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Inscrever-se em tags personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags subscritas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Define a lista de tags subscritas expostas ao aplicativo. </p> <p>Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas por meio de <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalize as tags de publicidade usadas pelo detector de oportunidade padrão  </b> </td> 
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

* Não é possível alterar a configuração após o carregamento do fluxo de mídia.

