---
description: Você pode especificar várias opções de estilo de legenda, e essas opções substituem as opções de estilo nas legendas originais.
title: Opções de estilo de legenda fechada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Opções de estilo de legenda fechada{#closed-caption-styling-options}

Você pode especificar várias opções de estilo de legenda, e essas opções substituem as opções de estilo nas legendas originais.

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>Nas opções que definem valores padrão (por exemplo, `DEFAULT`), esse valor refere-se à configuração quando a legenda foi originalmente especificada.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Formato </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Fonte </td> 
   <td colname="2"> <p>O tipo de fonte. </p> <p>Pode ser definido somente como um valor definido pela enumeração <span class="codeph"> TextFormat.Font </span> e representa, por exemplo, um espaçamento único com ou sem serifs. </p> <p>Dica:  As fontes reais disponíveis em um dispositivo podem variar, e as substituições são usadas quando necessário. O espaço único com serifs é normalmente utilizado como substituto, embora esta substituição possa ser específica do sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamanho </td> 
   <td colname="2"> <p>O tamanho da legenda. </p> <p> Pode ser definido somente como um valor definido pela enumeração <span class="codeph"> TextFormat.Size </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MÉDIO  </span> - O tamanho padrão </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE  </span> - Aproximadamente 30% maior que a média </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUENO  </span> - Aproximadamente 30% menor que o médio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT  </span> - O tamanho padrão da legenda; igual ao meio </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da fonte </td> 
   <td colname="2"> <p>A cor da fonte. </p> <p>Pode ser definido somente como um valor definido pela enumeração <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor do plano de fundo </td> 
   <td colname="2"> <p>A cor da célula do caractere de fundo. </p> <p>Pode ser definido somente para valores que estão disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade da fonte </td> 
   <td colname="2"> <p>A opacidade do texto. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> para a fonte é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Inset inferior </td> 
   <td colname="2"> <p>Distância vertical da parte inferior da janela da legenda para legendas a serem evitadas. </p> <p>Expressa como uma porcentagem da altura da janela da legenda (por exemplo, "20%") ou um número de pixels (por exemplo, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Área segura </td> 
   <td colname="2"> <p>Uma região ao redor da borda da tela entre 0% e 25%, onde as legendas não aparecerão. </p> <p>Por padrão, a área segura para 608/708 é de 12% e a área segura para WebVTT é de 0%. Essa configuração permite que seu aplicativo substitua esse padrão. Se dois valores forem fornecidos, por exemplo, a string "10%,20%", o primeiro valor será a área segura horizontal e o segundo valor será a área segura vertical. Se um valor for fornecido, por exemplo, a string "15%", os eixos vertical e horizontal usarão a área segura especificada. </p> </td> 
  </tr> 
 </tbody> 
</table>

