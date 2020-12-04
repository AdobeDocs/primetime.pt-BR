---
description: Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig.
seo-description: Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig.
seo-title: Métodos de classe Config para tags
title: Métodos de classe Config para tags
uuid: f2758085-8e49-4eaf-82bb-4a2e4dd8accb
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Métodos da classe Config para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig.

O TVSDK aplica a configuração global automaticamente a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`MediaPlayerItemConfig` expõe esses métodos para gerenciar as tags personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Assinar tags personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> string final pública[] getSubscribedTags()  </span> </td> 
   <td colname="col2"> Recupera a lista atual das tags assinadas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(tags String[]);  </span> </td> 
   <td colname="col2"> Define a lista de tags assinadas que serão expostas ao aplicativo. <p>Seu aplicativo também se inscreve automaticamente em todas as tags transmitidas por meio de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar as tags de publicidade usadas pelo detector de oportunidade padrão</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> string final pública[] getAdTags();  </span> </td> 
   <td colname="col2"> Recupera a lista atual de tags de anúncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(tags String[]);  </span> </td> 
   <td colname="col2"> Define a lista de tags de anúncio que serão usadas pelo gerador de oportunidade padrão. </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro tags contenha valores nulos.

   Se encontrado, o TVSDK lança um `IllegalArgumentException`.
* O nome da tag personalizada deve conter o prefixo #.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.
* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.

