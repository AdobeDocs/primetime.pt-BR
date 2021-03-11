---
description: Você pode fornecer informações de estilo para faixas de legenda fechada usando a classe TextFormat. Isso define o estilo para quaisquer legendas ocultas exibidas pelo seu reprodutor.
title: Controle o estilo da legenda oculta
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Controlar estilo de legenda {#control-closed-caption-styling-overview}

Você pode fornecer informações de estilo para faixas de legenda fechada usando a classe TextFormat. Isso define o estilo para quaisquer legendas ocultas exibidas pelo seu reprodutor.

Essa classe encapsula informações de estilo de legenda fechada, como tipo de fonte, tamanho, cor e opacidade do plano de fundo. Uma classe auxiliar associada, `TextFormatBuilder`, facilita o trabalho com configurações de estilo de legenda fechada.

## Definir estilos de legenda {#set-closed-caption-styles}

Você pode criar um estilo para o texto de legenda com métodos TVSDK.

1. Aguarde até que o reprodutor de mídia esteja pelo menos no estado PREPARADO.
1. Crie uma instância `TextFormatBuilder`.

   Você pode fornecer todos os parâmetros de estilo de legenda agora ou defini-los posteriormente.

   O TVSDK encapsula informações de estilo de legenda fechada na interface `TextFormat`. A classe `TextFormatBuilder` cria objetos que implementam essa interface.

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. Para obter uma referência a um objeto que implementa a interface `TextFormat`, chame o método público `TextFormatBuilder.toTextFormat`.

   Isso retorna um objeto `TextFormat` que pode ser aplicado ao reprodutor de mídia.

   ```java
   public TextFormat toTextFormat()
   ```

1. Opcionalmente, obtenha as configurações de estilo de legenda fechada atuais seguindo um destes procedimentos:

   * Obtenha todas as configurações de estilo com `MediaPlayer.getCCStyle`.

      O valor de retorno é uma instância da interface `TextFormat`.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * Obtenha as configurações, uma de cada vez, por meio dos métodos getter da interface `TextFormat`.

      ```js
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. Para alterar as configurações de estilo, siga um destes procedimentos:

   >[!NOTE]
   >
   >Não é possível alterar o tamanho das legendas da WebVTT.

   * Use o método setter `MediaPlayer.setCCStyle`, transmitindo uma instância da interface `TextFormat`:

      ```js
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

   * Use a classe `TextFormatBuilder`, que define métodos setter individuais.

      A interface `TextFormat` define um objeto imutável para que haja apenas métodos getter e nenhum setters. Você pode definir os parâmetros de estilo de legenda fechada somente com a classe `TextFormatBuilder` :

      ```js
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

A configuração do estilo de legenda oculta é uma operação assíncrona; portanto, pode levar até alguns segundos para que as alterações sejam exibidas na tela.

## Opções de estilo de legenda ocultas {#closed-caption-styling-options}

Você pode especificar várias opções de estilo de legenda, e essas opções substituem as opções de estilo nas legendas originais

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>Nas opções que definem valores padrão (por exemplo, DEFAULT), esse valor refere-se à configuração quando a legenda foi originalmente especificada.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Formato </b></th> 
   <th colname="2" class="entry"> <b>Descrição</b> </th> 
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
   <td colname="1"> Borda da fonte </td> 
   <td colname="2"> <p>O efeito usado para a borda da fonte, como acima ou não. </p> <p>Pode ser definido somente como um valor definido pela enumeração <span class="codeph"> TextFormat.FontEdge </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da fonte </td> 
   <td colname="2"> <p>A cor da fonte. </p> <p>Pode ser definido somente como um valor definido pela enumeração <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da borda </td> 
   <td colname="2"> <p>A cor do efeito da borda. </p> <p>Pode ser definido como qualquer um dos valores disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor do plano de fundo </td> 
   <td colname="2"> <p>A cor da célula do caractere de fundo. </p> <p>Pode ser definido somente para valores que estão disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor de preenchimento </td> 
   <td colname="2"> <p>A cor do plano de fundo da janela em que o texto está localizado. </p> <p>Pode ser definido como qualquer um dos valores disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade da fonte </td> 
   <td colname="2"> <p>A opacidade do texto. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> para a fonte é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade de fundo </td> 
   <td colname="2"> <p>A opacidade da célula do caractere de plano de fundo. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> para o plano de fundo é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade de preenchimento </td> 
   <td colname="2"> <p>A opacidade do plano de fundo da janela da legenda. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> para preenchimento é 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exemplos de formatação de legenda {#examples-caption-formatting}

É possível especificar a formatação de legenda oculta.

**Exemplo 1: Especificar valores de formato explicitamente**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**Exemplo 2: Especificar valores de formato em parâmetros**

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
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
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
