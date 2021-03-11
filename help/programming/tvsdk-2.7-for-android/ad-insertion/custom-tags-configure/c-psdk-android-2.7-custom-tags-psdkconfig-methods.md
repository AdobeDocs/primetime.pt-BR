---
description: Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig .
title: Métodos da classe Config para tags
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Métodos de classe de configuração para tags {#config-class-methods-for-tags}

Você pode configurar globalmente nomes de tags personalizados no TVSDK com a classe MediaPlayerItemConfig .

O TVSDK aplica automaticamente a configuração global a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`MediaPlayerItemConfig` expõe esses métodos para gerenciar as tags personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Inscrever-se em tags personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> string final pública[] getSubscribedTags  </span> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags subscritas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> público final void setSubscribedTags(String[] tags);  </span> </td> 
   <td colname="col2"> <p>Define a lista de tags assinadas que serão expostas ao aplicativo. </p> <p>Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas por meio de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalize as tags de publicidade usadas pelo detector de oportunidade padrão</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> cadeia final pública[] getAdTags;  </span> </td> 
   <td colname="col2"> <p>Recupera a lista atual de tags de anúncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> público final void setAdTags(String[] tags);  </span> </td> 
   <td colname="col2"> <p>Define a lista de tags de anúncio que serão usadas pelo gerador de oportunidade padrão. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro de tags contenha valores nulos.

   Se encontrado, o TVSDK lança um `IllegalArgumentException`.
* O nome da tag personalizada deve conter o prefixo `#`.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.

* Não é possível alterar a configuração após o carregamento do fluxo de mídia.
