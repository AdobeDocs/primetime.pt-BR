---
description: É possível especificar várias opções de estilo de legenda, e essas opções substituem as opções de estilo nas legendas originais.
title: Opções de estilo de legendas ocultas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Opções de estilo de legendas ocultas{#closed-caption-styling-options}

É possível especificar várias opções de estilo de legenda, e essas opções substituem as opções de estilo nas legendas originais.

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
>Nas opções que definem valores padrão (por exemplo, `DEFAULT`), esse valor se refere ao que era a configuração quando a legenda foi originalmente especificada.

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
   <td colname="2"> <p>O tipo de fonte. </p> <p>Pode ser definido somente como um valor definido pela variável <span class="codeph"> FormatoTexto.Fonte </span> enumeração e representa, por exemplo, monospaced com ou sem serifas. </p> <p>Dica: as fontes reais disponíveis em um dispositivo podem variar, e as substituições são usadas quando necessário. O monoespaço com serifas é normalmente usado como um substituto, embora essa substituição possa ser específica do sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamanho </td> 
   <td colname="2"> <p>O tamanho da legenda. </p> <p> Pode ser definido somente como um valor definido pelo <span class="codeph"> FormatoTexto.Tamanho </span> enumeração: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MÉDIO </span> - O tamanho padrão </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE </span> - Aproximadamente 30% maior que o médio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUENO </span> - Aproximadamente 30% menor que o médio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PADRÃO </span> - O tamanho padrão da legenda; o mesmo que o médio </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da fonte </td> 
   <td colname="2"> <p>A cor da fonte. </p> <p>Pode ser definido somente como um valor definido pelo <span class="codeph"> FormatoDeTexto.Cor </span> lista discriminada. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor do plano de fundo </td> 
   <td colname="2"> <p>A cor da célula do caractere de plano de fundo. </p> <p>Pode ser definido somente para valores que estão disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade da fonte </td> 
   <td colname="2"> <p>A opacidade do texto. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY </span> para a fonte, é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Inserção inferior </td> 
   <td colname="2"> <p>Distância vertical a partir da parte inferior da janela de legenda para evitar legendas. </p> <p>Expressa como uma porcentagem da altura da janela da legenda (por exemplo, "20%") ou um número de pixels (por exemplo, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Área de segurança </td> 
   <td colname="2"> <p>Uma região ao redor da borda da tela entre 0% e 25% em que as legendas não serão exibidas. </p> <p>Por padrão, a área segura para 608/708 é de 12% e a área segura para WebVTT é de 0%. Essa configuração permite que o aplicativo substitua esse padrão. Se dois valores forem fornecidos, por exemplo, a string "10%,20%", o primeiro valor será a área segura horizontal e o segundo valor será a área segura vertical. Se um valor for fornecido, por exemplo, a string "15%", ambos os eixos vertical e horizontal usarão a área segura especificada. </p> </td> 
  </tr> 
 </tbody> 
</table>
