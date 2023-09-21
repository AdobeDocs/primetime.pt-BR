---
description: O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.
title: Definir tempos de buffering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Definir tempos de buffering{#set-buffering-times}

O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o reprodutor de mídia assumirá como padrão 2 segundos para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configurar o `BufferControlParameters` objeto, que encapsula o tempo de buffer inicial e os parâmetros de controle do tempo de buffer de reprodução:

       Essa classe fornece os seguintes métodos de fábrica:
   
   * Para definir o tempo de buffer inicial igual ao tempo de buffer de reprodução:

     ```
     createSimple(bufferTime:uint):BufferControlParameters
     ```

   * Para definir os tempos de buffer inicial e de reprodução:

     ```
     createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
     ```

     Esses métodos lançam um `IllegalArgumentException` se os parâmetros não forem válidos, como quando:

   * O tempo de buffer inicial é menor que zero.
   * O tempo de buffer inicial é maior que o tempo de buffer.

1. Para definir os valores de parâmetro de buffer, use esta opção `MediaPlayer` método:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Para obter os valores atuais de parâmetro de buffer, use este `MediaPlayer` método:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por exemplo, para definir o buffer inicial como 2 segundos e o tempo de buffer de reprodução como 30 segundos:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

A variável `psdkdemo` demonstra esse recurso; use as configurações do aplicativo para definir os valores de buffer.
