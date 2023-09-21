---
description: Você pode configurar nomes de tag personalizados em um fluxo com a classe MediaPlayerItemConfig.
title: Métodos de classe de configuração para tags
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Métodos de classe de configuração para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tag personalizados em um fluxo com a classe MediaPlayerItemConfig.

Para criar um novo `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

Estas são algumas informações sobre como o `MediaPlayerItemConfig` Os métodos são usados para gerenciar tags personalizadas:

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
   <td colname="col2"> <p>Recupera a lista atual de tags assinadas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Define a lista de tags assinadas expostas ao aplicativo. </p> <p>Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas pelo <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar as tags de publicidade usadas pelo detector de oportunidades padrão </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags de anúncios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>Define a lista de tags de anúncio a ser usada pelo gerador de oportunidades padrão. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* O nome da tag personalizada deve conter a `#` prefixo.

  Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.
