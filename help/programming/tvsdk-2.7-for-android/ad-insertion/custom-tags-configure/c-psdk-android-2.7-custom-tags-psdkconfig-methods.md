---
description: É possível configurar globalmente nomes de tag personalizados no TVSDK com a classe MediaPlayerItemConfig.
title: Métodos de classe de configuração para tags
exl-id: 48e88284-788c-49b3-a370-3e3d77a8da6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Métodos de classe de configuração para tags {#config-class-methods-for-tags}

É possível configurar globalmente nomes de tag personalizados no TVSDK com a classe MediaPlayerItemConfig.

O TVSDK aplica automaticamente a configuração global a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`MediaPlayerItemConfig` O expõe estes métodos para gerenciar tags personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Assinar tags personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> String final pública[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags assinadas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public void setSubscribedTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>Define a lista de tags assinadas que serão expostas ao aplicativo. </p> <p>Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas pelo <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar as tags de publicidade usadas pelo detector de oportunidades padrão</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> String final pública[] getAdTags; </span> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags de anúncios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public void setAdTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>Define a lista de tags de anúncios que serão usadas pelo gerador de oportunidades padrão. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro de tags contenha valores nulos.

   Se encontrado, o TVSDK lança um `IllegalArgumentException`.
* O nome da tag personalizada deve conter a `#` prefixo.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.
