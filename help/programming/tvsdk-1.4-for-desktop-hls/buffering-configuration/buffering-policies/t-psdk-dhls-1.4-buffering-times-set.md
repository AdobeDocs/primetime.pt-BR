---
description: O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering da reprodução.
seo-description: O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering da reprodução.
seo-title: Definir tempos de buffering
title: Definir tempos de buffering
uuid: 25142b01-5381-49c9-b89a-24c858faaf13
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Definir tempos de buffering{#set-buffering-times}

O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering da reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o player de mídia assumirá 2 segundos como padrão para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configure o objeto `BufferControlParameters`, que encapsula os parâmetros de controle de tempo do buffer inicial e do buffer de reprodução:

       Esta classe fornece os seguintes métodos de fábrica:
   
   * Para definir o tempo inicial do buffer igual ao tempo do buffer de reprodução:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Para definir os tempos de buffer inicial e de reprodução:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Esses métodos exibem um `IllegalArgumentException` se os parâmetros não forem válidos, como quando:

   * O tempo inicial do buffer é menor que zero.
   * O tempo inicial do buffer é maior que o tempo do buffer.

1. Para definir os valores dos parâmetros de buffer, use este método `MediaPlayer`:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Para obter os valores de parâmetro de buffer atuais, use este método `MediaPlayer`:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por exemplo, para definir o buffer inicial para 2 segundos e o tempo do buffer de reprodução para 30 segundos:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

O `psdkdemo` demonstra este recurso; use as configurações do aplicativo para definir os valores do buffer.
