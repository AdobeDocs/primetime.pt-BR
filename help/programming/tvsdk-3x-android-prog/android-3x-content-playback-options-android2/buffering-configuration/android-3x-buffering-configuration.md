---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar como o player é armazenado em buffer.
seo-description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar como o player é armazenado em buffer.
seo-title: Buffering
title: Buffering
uuid: c84b98ed-0070-4a86-a409-d7702e5be23c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visão geral {#buffering-overview}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar como o player é armazenado em buffer.

O TVSDK define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial antes da reprodução da mídia, de pelo menos 2 segundos. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para proporcionar um início suave quando a reprodução é iniciada.

Você pode alterar os tempos do buffer definindo novas políticas de buffering e pode alterar quando o buffering inicial ocorrer usando instantaneamente.

## Políticas de tempo de buffer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições da rede), você pode definir diferentes políticas de buffering para o player, como alterar a duração mínima para buffering inicial e para buffering contínuo de reprodução.

Depois de ligar `play`, o player de mídia inicia o buffering do vídeo. Quando o player de mídia armazena em buffer a quantidade de vídeo especificada pelo tempo inicial do buffer, a reprodução é iniciada. Esse processo melhora o tempo de inicialização porque o player não espera que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, após os poucos segundos iniciais serem armazenados em buffer, a reprodução é iniciada.

Enquanto o vídeo está sendo renderizado, o TVSDK continua a armazenar em buffer novos fragmentos até que ele tenha armazenado em buffer a quantidade especificada pelo tempo do buffer de reprodução. Se o tamanho atual do buffer cair abaixo do tempo de buffer de reprodução, o player baixará fragmentos adicionais. Quando a duração atual do buffer estiver acima do tempo do buffer de reprodução em alguns segundos, o TVSDK interromperá o download dos fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um tempo de buffering inicial longo antes de iniciar. Isso pode propiciar uma reprodução suave por mais tempo. no entanto, se as condições da rede forem precárias, a reprodução inicial poderá ser atrasada.

Se você ativar a ativação imediata ao chamar `prepareBuffer`, o buffering inicial começará nesse momento, em vez de esperar `play`.

## Definir tempos de buffering {#section_05CDD927869D47EBA1D2069B1416B2E4}

O `MediaPlayer` fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering da reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o player de mídia assumirá 2 segundos como padrão para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configure o `BufferControlParameters` objeto, que encapsula o tempo de buffer inicial e os parâmetros de controle de tempo do buffer de reprodução.

   Esta classe fornece os seguintes métodos de fábrica:

   * Para definir o tempo inicial do buffer igual ao tempo do buffer de reprodução:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Para definir os tempos de buffer inicial e de reprodução:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Se os parâmetros não forem válidos, esses métodos serão lançados `MediaPlayerException` com o código de erro `PSDKErrorCode.INVALID_ARGUMENT`, como quando as seguintes condições forem atendidas:

   * O tempo inicial do buffer é menor que zero.
   * O tempo inicial do buffer é maior que o tempo do buffer.


1. Para definir os valores dos parâmetros de buffer, use este `MediaPlayer` método:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obter os valores de parâmetro de buffer atuais, use este `MediaPlayer` método:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Por exemplo, para definir o buffer inicial para 5 segundos e o tempo do buffer de reprodução para 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
