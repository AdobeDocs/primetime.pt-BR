---
description: Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig ou com base em fluxo com a classe MediaPlayerItemConfig.
seo-description: Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig ou com base em fluxo com a classe MediaPlayerItemConfig.
seo-title: Métodos de classe Config para tags
title: Métodos de classe Config para tags
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

---


# Métodos de classe Config para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tags personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig ou com base em fluxo com a classe MediaPlayerItemConfig.

O TVSDK aplica a configuração global automaticamente a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

Ambos `PSDKConfig` e `MediaPlayerItemConfig` expomos esses métodos para gerenciar as tags personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Assinar tags personalizadas específicas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> função pública get subscribeTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera a lista atual de tags assinadas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> conjunto de funções públicas subscribeTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2">Define a lista de tags assinadas que serão expostas ao aplicativo. <p>Seu aplicativo também se inscreve automaticamente em todas as tags transmitidas por meio de <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalizar as tags de publicidade usadas pelo detector de oportunidade padrão </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> função pública get adTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera a lista atual de tags de publicidade. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> função pública set adTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2"> Define a lista de tags de publicidade que serão usadas pelo gerador de oportunidade padrão. </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro tags contenha valores nulos.

   Se encontrado, o TVSDK emite um `IllegalArgumentException`.
* O nome da tag personalizada deve conter o prefixo #.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.
* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.

