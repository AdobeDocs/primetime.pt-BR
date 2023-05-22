---
description: Você pode configurar nomes de tag personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig ou baseado em fluxo com a classe MediaPlayerItemConfig.
title: Métodos de classe de configuração para tags
exl-id: 093720df-9c2d-41f1-ba9d-9553c5df40a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Métodos de classe de configuração para tags{#config-class-methods-for-tags}

Você pode configurar nomes de tag personalizados no TVSDK globalmente com a classe MediaPlayerItemConfig ou baseado em fluxo com a classe MediaPlayerItemConfig.

O TVSDK aplica a configuração global automaticamente a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

Ambos `PSDKConfig` e `MediaPlayerItemConfig` exponha estes métodos para gerenciar tags personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Assinar tags personalizadas específicas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> função public get subscribeTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera a lista atual de tags assinadas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> função pública definida subscribeTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2">Define a lista de tags assinadas que serão expostas ao aplicativo. <p>Seu aplicativo também é automaticamente inscrito em todas as tags transmitidas pelo <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalizar as tags de publicidade usadas pelo detector de oportunidades padrão </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> função public get adTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera a lista atual de tags de anúncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set adTags():Vetor.&lt;String&gt;</span> </td> 
   <td colname="col2"> Define a lista de tags de anúncios que serão usadas pelo gerador de oportunidades padrão. </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro de tags contenha valores nulos.

   Se encontrado, o TVSDK lança um `IllegalArgumentException`.
* O nome da tag personalizada deve conter o prefixo #.

   Por exemplo, `#EXT-X-ASSET` é um nome de tag personalizado correto, mas `EXT-X-ASSET` está incorreto.
* Não é possível alterar a configuração depois que o fluxo de mídia é carregado.
