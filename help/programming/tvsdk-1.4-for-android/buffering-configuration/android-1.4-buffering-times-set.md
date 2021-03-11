---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.
title: Definir tempos de buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Buffering {#buffering}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.

O TVSDK define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial de pelo menos 2 segundos durante a reprodução da mídia. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para fornecer um início suave quando realmente começa a reproduzir.

Você pode alterar os tempos do buffer definindo novas políticas de buffering e pode alterar quando o buffering inicial ocorrer usando o instantâneo.

## Definir tempos de buffering {#set-buffering-times}

O `MediaPlayer` fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o padrão do reprodutor de mídia será 2 segundos para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configure o objeto `BufferControlParameters`, que encapsula o tempo de buffer inicial e os parâmetros de controle de tempo do buffer de reprodução:

       Esta classe fornece dois métodos de fábrica:
   
   * Para definir o tempo de buffer inicial igual ao tempo de buffer de reprodução:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Para definir os tempos de buffer inicial e de reprodução:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Esses métodos exibem um `IllegalArgumentException` se os parâmetros não forem válidos, como quando:

   * O tempo de buffer inicial é menor que zero.
   * O tempo de buffer inicial é maior que o tempo de buffer.

1. Para definir os valores dos parâmetros de buffer, use este método `MediaPlayer`:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obter os valores atuais dos parâmetros de buffer, use este método `MediaPlayer`:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Se o AVE não puder definir os valores especificados, o reprodutor de mídia entrará no estado `ERROR` com o código de erro `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por exemplo, para definir o buffer inicial como 2 segundos e o tempo do buffer de reprodução como 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

A implementação de referência do Primetime demonstra esse recurso; use as configurações do aplicativo para definir os valores do buffer.