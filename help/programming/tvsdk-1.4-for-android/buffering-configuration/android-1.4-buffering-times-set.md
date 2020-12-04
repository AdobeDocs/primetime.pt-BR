---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.
seo-description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.
seo-title: Definir tempos de buffering
title: Definir tempos de buffering
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Buffering {#buffering}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.

O TVSDK define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial de pelo menos 2 segundos antes da reprodução dos start de mídia. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para fornecer um start suave quando ela é realmente start.

Você pode alterar os tempos do buffer definindo novas políticas de buffering e pode alterar quando o buffering inicial ocorrer usando o instantâneo.

## Definir tempos de buffering {#set-buffering-times}

O `MediaPlayer` fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering da reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o player de mídia assumirá 2 segundos como padrão para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configure o objeto `BufferControlParameters`, que encapsula os parâmetros de controle de tempo do buffer inicial e do buffer de reprodução:

       Esta classe fornece dois métodos de fábrica:
   
   * Para definir o tempo inicial do buffer igual ao tempo do buffer de reprodução:

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

   * O tempo inicial do buffer é menor que zero.
   * O tempo inicial do buffer é maior que o tempo do buffer.

1. Para definir os valores dos parâmetros de buffer, use este método `MediaPlayer`:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obter os valores de parâmetro de buffer atuais, use este método `MediaPlayer`:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Se o AVE não puder definir os valores especificados, o player de mídia inserirá o estado `ERROR` com o código de erro `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por exemplo, para definir o buffer inicial para 2 segundos e o tempo do buffer de reprodução para 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

A implementação da referência Primetime demonstra esta característica; use as configurações do aplicativo para definir os valores do buffer.