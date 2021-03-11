---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o buffering do reprodutor.
title: Buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Visão geral {#buffering-overview}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o buffering do reprodutor.

O TVSDK define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial antes da reprodução da mídia, de pelo menos 2 segundos. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para fornecer um início suave quando realmente começa a reproduzir.

Você pode alterar os tempos do buffer definindo novas políticas de buffering e pode alterar quando o buffering inicial ocorrer usando o instantâneo em.

## Políticas de tempo de buffer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições de rede), você pode definir diferentes políticas de buffering para o seu reprodutor, como alterar a duração mínima para buffering inicial e para buffering de reprodução contínua.

Depois de chamar `play`, o reprodutor de mídia inicia o buffer do vídeo. Quando o reprodutor de mídia armazena em buffer a quantidade de vídeo especificada pelo tempo inicial do buffer, a reprodução começa. Esse processo melhora o tempo de inicialização, pois o reprodutor não espera que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, depois que os poucos segundos iniciais são armazenados em buffer, a reprodução começa.

Enquanto o vídeo é renderizado, o TVSDK continua armazenando novos fragmentos em buffer até que ele tenha colocado em buffer a quantidade especificada pelo tempo do buffer de reprodução. Se o comprimento atual do buffer cair abaixo do tempo do buffer de reprodução, o reprodutor baixará fragmentos adicionais. Depois que o comprimento atual do buffer estiver acima do tempo do buffer de reprodução em alguns segundos, o TVSDK interromperá o download dos fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um longo tempo inicial de buffering antes de iniciar. Isso pode proporcionar uma reprodução suave por mais tempo; no entanto, se as condições da rede forem precárias, a reprodução inicial poderá ser adiada.

Se você ativar o instantâneo ao chamar `prepareBuffer`, o buffering inicial começará nesse momento, em vez de esperar por `play`.

## Definir tempos de buffering {#section_05CDD927869D47EBA1D2069B1416B2E4}

O `MediaPlayer` fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o padrão do reprodutor de mídia será 2 segundos para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configure o objeto `BufferControlParameters`, que encapsula o tempo de buffer inicial e os parâmetros de controle de tempo do buffer de reprodução.

   Esta classe fornece os seguintes métodos de fábrica:

   * Para definir o tempo de buffer inicial igual ao tempo de buffer de reprodução:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Para definir os tempos de buffer inicial e de reprodução:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Se os parâmetros não forem válidos, esses métodos acionarão `MediaPlayerException` com o código de erro `PSDKErrorCode.INVALID_ARGUMENT`, como quando as seguintes condições forem atendidas:

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Por exemplo, para definir o buffer inicial como 5 segundos e o tempo do buffer de reprodução como 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
