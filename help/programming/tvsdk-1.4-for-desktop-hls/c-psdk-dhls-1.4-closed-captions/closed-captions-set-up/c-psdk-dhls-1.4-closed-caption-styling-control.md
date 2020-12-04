---
description: Você pode fornecer informações de estilização para faixas de legenda fechada usando a classe ClosedCaptionStyles. Isso define o estilo de todas as legendas ocultas exibidas pelo player.
seo-description: Você pode fornecer informações de estilização para faixas de legenda fechada usando a classe ClosedCaptionStyles. Isso define o estilo de todas as legendas ocultas exibidas pelo player.
seo-title: Controlar estilo de legenda
title: Controlar estilo de legenda
uuid: 506c06d3-8fe0-46c9-9ed6-5b35d21c021c
translation-type: tm+mt
source-git-commit: b67a9dcb0abb07f4fdff4e03d9d6c0b07ff45127
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---


# Controlar estilização de legenda fechada{#control-closed-caption-styling}

Você pode fornecer informações de estilização para faixas de legenda fechada usando a classe ClosedCaptionStyles. Isso define o estilo de todas as legendas ocultas exibidas pelo player.

Essa classe encapsula informações de estilo de legenda fechada, como tipo de fonte, tamanho, cor e opacidade de plano de fundo. Uma classe auxiliar associada, `ClosedCaptionStylesBuilder`, facilita o trabalho com configurações de estilo de legenda fechada.

## Definir estilos de legenda fechada {#section_DAE84659D1964DB1B518F91B59AF29D9}

É possível criar o estilo do texto de legenda com métodos TVSDK.

1. Aguarde até que o MediaPlayer tenha pelo menos o status PREPARED (consulte [Aguarde um estado válido](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Para alterar as configurações de estilo, execute um dos procedimentos a seguir:

   * Use a classe auxiliar `ClosedCaptionStylesBuilder` (opera em `ClosedCaptionStyles` nos bastidores).
   * Use a classe `ClosedCaptionStyles` diretamente.

>[!NOTE]
>
>A configuração do estilo de legenda fechada é uma operação assíncrona, portanto, pode levar até alguns segundos para que as alterações sejam exibidas na tela.

## Opções de estilo de legenda fechada {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

Você pode fornecer informações de estilização para faixas de legenda fechada usando a classe `ClosedCaptionStyles`. Isso define o estilo de todas as legendas ocultas exibidas pelo player.

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
```

>[!TIP]
>
>Nas opções que definem valores padrão (por exemplo, `DEFAULT`), esse valor se refere ao que a configuração era quando a legenda foi originalmente especificada.

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
   <td colname="2"> <p>O tipo de fonte. </p> <p>Pode ser definido somente para um valor definido pela matriz <span class="codeph"> ClosedCaptionStyles.FONT </span> e representa, por exemplo, espaçados com ou sem serifs. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>Dica:  As fontes reais disponíveis em um dispositivo podem variar e as substituições são usadas quando necessário. O espaço único com serifs é normalmente utilizado como substituto, embora essa substituição possa ser específica do sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Tamanho </td> 
   <td colname="2"> <p>O tamanho da legenda. </p> <p> Pode ser definido somente para um valor definido pela matriz <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MÉDIO  </span> - Tamanho normal </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE  </span> - Aproximadamente 30% maior que a média </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PEQUENO  </span> - Aproximadamente 30% menor que o médio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PADRÃO  </span> - O tamanho padrão da legenda; igual ao meio </li> 
     </ul> </p> <p>Dica:  Você pode alterar o tamanho da fonte das legendas WebVTT alterando o parâmetro de tamanho para a função <span class="codeph"> DefaultMediaPlayer.ccStyles setter </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Borda da fonte </td> 
   <td colname="2"> <p>O efeito usado para a borda da fonte, como elevado ou nenhum. </p> <p>Pode ser definido somente para um valor definido pela matriz <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span>. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da fonte </td> 
   <td colname="2"> <p>A cor da fonte. </p> <p>Pode ser definido somente para um valor definido pela matriz <span class="codeph"> ClosedCaptionStyles.COLOR </span>. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da borda </td> 
   <td colname="2"> <p>A cor do efeito da borda. </p> <p>Pode ser definido para qualquer um dos valores disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor do plano de fundo </td> 
   <td colname="2"> <p>A cor da célula do caractere de plano de fundo. </p> <p>Pode ser definido somente para valores que estão disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor de preenchimento </td> 
   <td colname="2"> <p>A cor do plano de fundo da janela na qual o texto está localizado. </p> <p>Pode ser definido para qualquer um dos valores disponíveis para a cor da fonte. </p> <p>Importante:  Isso não se aplica às legendas WebVTT, pois a WebVTT não usa esse recurso. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade da fonte </td> 
   <td colname="2"> <p>A opacidade do texto. </p> <p>Expresso como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para a fonte é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade do plano de fundo </td> 
   <td colname="2"> <p>A opacidade da célula de caractere de plano de fundo. </p> <p>Expresso como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para o plano de fundo é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade de preenchimento </td> 
   <td colname="2"> <p>A opacidade do plano de fundo da janela da legenda. </p> <p>Expresso como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> para preenchimento é 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exemplos: Formatação de legenda {#section_63E33840B7A14D26990046E2ACF2ECA1}

É possível especificar a formatação de legenda fechada.

## Exemplo 1: Especificar valores de formato explicitamente {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## Exemplo 2: Especificar valores de formato nos parâmetros {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity 
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity. 
*/ 
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
