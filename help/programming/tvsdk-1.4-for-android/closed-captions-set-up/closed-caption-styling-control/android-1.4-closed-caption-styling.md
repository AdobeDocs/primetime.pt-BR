---
description: Você pode fornecer informações de estilo para faixas de legendas ocultas usando a classe TextFormat. Isso define o estilo de todas as legendas ocultas exibidas pelo reprodutor.
title: Controlar estilo de legendas ocultas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Controlar estilo de legendas ocultas {#control-closed-caption-styling-overview}

Você pode fornecer informações de estilo para faixas de legendas ocultas usando a classe TextFormat. Isso define o estilo de todas as legendas ocultas exibidas pelo reprodutor.

Essa classe encapsula informações de estilo de legendas ocultas, como tipo de fonte, tamanho, cor e opacidade do plano de fundo. Uma classe auxiliar associada, `TextFormatBuilder`, facilita o trabalho com configurações de estilo de legenda oculta.

## Definir estilos de legendas ocultas {#set-closed-caption-styles}

É possível estilizar o texto de legenda oculta com métodos TVSDK.

1. Aguarde até que o reprodutor de mídia esteja pelo menos no estado PREPARADO.
1. Criar um `TextFormatBuilder` instância.

   Você pode fornecer todos os parâmetros de estilo de legendas ocultas agora ou defini-los posteriormente.

   O TVSDK encapsula informações de estilo de legendas ocultas no `TextFormat` interface. A variável `TextFormatBuilder` A classe cria objetos que implementam essa interface.

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

1. Para obter uma referência a um objeto que implemente a variável `TextFormat` , chame o `TextFormatBuilder.toTextFormat` método público.

   Isso retorna um `TextFormat` objeto que pode ser aplicado ao reprodutor de mídia.

   ```java
   public TextFormat toTextFormat()
   ```

1. Como opção, obtenha as configurações de estilo atuais de legenda oculta seguindo um destes procedimentos:

   * Obter todas as configurações de estilo com `MediaPlayer.getCCStyle`.

     O valor de retorno é uma instância do `TextFormat` interface.

     ```js
     /** 
     * @return the current closed captioning style.  
     * If no style was previously set, it returns a TextFormat object 
     * with default values for each attribute. 
     * @throws IllegalStateException if media player was already released. 
     */ 
     public TextFormat getCCStyle() throws IllegalStateException;
     ```

   * Obtenha as configurações, uma de cada vez, por meio da `TextFormat` métodos getter da interface.

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
   >Não é possível alterar o tamanho das legendas WebVTT.

   * Usar o método setter `MediaPlayer.setCCStyle`, transmitindo uma instância do `TextFormat` interface:

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

   * Use o `TextFormatBuilder` classe, que define métodos setter individuais.

     A variável `TextFormat` A interface define um objeto imutável para que haja apenas métodos Getter e nenhum setters. É possível definir os parâmetros de estilo de legenda oculta somente com a `TextFormatBuilder` classe:

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

A configuração do estilo de legenda oculta é uma operação assíncrona, portanto, pode levar alguns segundos para que as alterações apareçam na tela.

## Opções de estilo de legendas ocultas {#closed-caption-styling-options}

É possível especificar várias opções de estilo de legenda, e essas opções substituem as opções de estilo nas legendas originais

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
>Nas opções que definem valores padrão (por exemplo, PADRÃO), esse valor se refere ao que era a configuração quando a legenda foi especificada originalmente.

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
   <td colname="1"> Borda da fonte </td> 
   <td colname="2"> <p>O efeito usado para a borda da fonte, como elevado ou nenhum. </p> <p>Pode ser definido somente como um valor definido pela variável <span class="codeph"> FormatoTexto.BordaFonte </span> lista discriminada. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da fonte </td> 
   <td colname="2"> <p>A cor da fonte. </p> <p>Pode ser definido somente como um valor definido pelo <span class="codeph"> FormatoDeTexto.Cor </span> lista discriminada. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor da borda </td> 
   <td colname="2"> <p>A cor do efeito de borda. </p> <p>Pode ser definido como qualquer um dos valores disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor do plano de fundo </td> 
   <td colname="2"> <p>A cor da célula do caractere de plano de fundo. </p> <p>Pode ser definido somente para valores que estão disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Cor de preenchimento </td> 
   <td colname="2"> <p>A cor do plano de fundo da janela em que o texto está localizado. </p> <p>Pode ser definido como qualquer um dos valores disponíveis para a cor da fonte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade da fonte </td> 
   <td colname="2"> <p>A opacidade do texto. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY </span> para a fonte, é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade do plano de fundo </td> 
   <td colname="2"> <p>A opacidade da célula de caractere do plano de fundo. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY </span> para o fundo é 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacidade de preenchimento </td> 
   <td colname="2"> <p>A opacidade do plano de fundo da janela de legenda. </p> <p>Expressa como uma porcentagem de 0 (totalmente transparente) a 100 (totalmente opaco). <span class="codeph"> DEFAULT_OPACITY </span> para preenchimento é 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exemplos de formatação da legenda {#examples-caption-formatting}

Você pode especificar a formatação de legendas ocultas.

**Exemplo 1: especificar explicitamente valores de formato**

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

**Exemplo 2: especificar valores de formato em parâmetros**

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
