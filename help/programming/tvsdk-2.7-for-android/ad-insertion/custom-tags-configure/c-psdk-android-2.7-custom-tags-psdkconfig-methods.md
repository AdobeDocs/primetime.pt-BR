---
description: Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig.
seo-description: Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig.
seo-title: Métodos de classe Config para tags
title: Métodos de classe Config para tags
uuid: 64284876-1f31-47e0-a99b-3bfe17e10707
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Métodos de classe Config para tags {#config-class-methods-for-tags}

Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig.

O TVSDK aplica automaticamente a configuração global a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`MediaPlayerItemConfig` expõe esses métodos para gerenciar as tags personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Assinar tags personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> string final pública[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags assinadas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(tags String[]); </span> </td> 
   <td colname="col2"> <p>Define a lista de tags assinadas que serão expostas ao aplicativo. </p> <p>Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas por meio de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar as tags de publicidade usadas pelo detector de oportunidade padrão</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> string final pública[] getAdTags; </span> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags de publicidade. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(tags String[]); </span> </td> 
   <td colname="col2"> <p>Define a lista de tags de publicidade que serão usadas pelo gerador de oportunidade padrão. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro tags contenha valores nulos.

   Se encontrado, o TVSDK emite um `IllegalArgumentException`.
* O nome da tag personalizada deve conter o `#` prefixo.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.
