---
description: Esta seção aborda a gramática da entrada de configuração, enfatizando opções de entrada válidas e inválidas e explicando como os campos opcionais omitidos são interpretados.
title: RBOP Gramática
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# RBOP Gramática {#rbop-grammar}

Esta seção aborda a gramática da entrada de configuração, enfatizando opções de entrada válidas e inválidas e explicando como os campos opcionais omitidos são interpretados.

A gramática de proteção de saída baseada em resolução é definida como uma sequência de regras, em que cada regra pode ter várias formas válidas:

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## Aplicação das regras gramaticais {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>Para ajudar a melhorar a legibilidade da gramática, as seguintes propriedades não são refletidas na gramática, mas ainda são verdadeiras:

1. A ordem dos pares definidos nos objetos não é fixa; assim, qualquer permuta dos pares é válida.

   Por exemplo, se definirmos um objeto como este:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   então, a seguinte estrutura também seria considerada válida: =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. Para cada par dentro de um objeto, presume-se que apenas uma instância desse par exista em uma determinada instância de um determinado objeto.

   Por exemplo, se definirmos um objeto como este:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   a instância a seguir seria inválida, pois há dois pares `foo` no mesmo objeto:

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   Da mesma forma, ter dois objetos como:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   e:

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   é válido, pois são instâncias independentes do mesmo objeto.

1. Para definições em que uma ou mais de uma sequência de cadeias de caracteres podem ser escolhidas, trate as cadeias de caracteres como um conjunto, em que as entradas duplicadas são tratadas como uma única entrada. Por exemplo, `["foo", "bar", "foo", "baz"]` é equivalente a `["foo", "bar", "baz"]`

1. Para definir números, um espaço é usado entre as regras, (por exemplo, `Digit Digits`), mas esse espaço não deve ser usado ao aplicar a regra.

   Por exemplo, se expressarmos o número *cento e vinte e três* de acordo com a regra NonZeroInteger, ele deverá ser expresso como `123` em vez de `1 2 3`, mesmo que a regra contenha um espaço entre NonZeroDigit e Digits.

1. Algumas das regras permitem vários formulários. Nesses casos, os diferentes formulários são separados pelo caractere `'|'`.

   Por exemplo, esta regra:

   ```
   Foo ::= "A" | "B" | "C"
   ```

   significa que uma instância de `Foo` pode ser substituída por &quot;A&quot;, &quot;B&quot; ou &quot;C&quot;. Não deve ser confundido com um formulário que abrange várias linhas; esse é um recurso que torna os formulários mais longos mais legíveis.

## A Gramática {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## Semântica: Configurações legais, mas inválidas {#section_709BE240FF0041D4A1B0A0A7544E4966}

O tópico *Exemplo de configuração de proteção de saída* apresentou uma configuração válida junto com seu significado semântico. A seção anterior no tópico *this* apresentava as regras gramaticais das configurações. Embora a gramática ajude a garantir o correto sintático, há configurações sintaticamente legais que não são semanticamente corretas (ou seja, não são lógicas). Esta seção apresenta configurações *sintaticamente* legais, mas *semântica* incorretas. Lembre-se de que os exemplos nesta seção foram reduzidos à estrutura mínima necessária para ilustrar o cenário em discussão.

* É inválido definir várias restrições de pixel com a mesma contagem de pixels.

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* Uma contagem de pixels não deve exceder a resolução máxima de pixels especificada.

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
