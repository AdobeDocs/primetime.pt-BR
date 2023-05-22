---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar como o reprodutor é armazenado em buffer.
title: Buffering
exl-id: f4df3084-376e-421c-aaa5-83de2815dabe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Visão geral {#buffering-overview}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar como o reprodutor é armazenado em buffer.

O TVSDK define um tamanho de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial antes de a mídia começar a ser reproduzida, de pelo menos 2 segundos. Depois que o aplicativo chamar `play`, mas antes de começar a reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para fornecer um início suave quando ela realmente começa a ser reproduzida.

Você pode alterar os tempos de buffer definindo novas políticas de buffering e pode alterar quando o buffering inicial ocorre usando instant on.

## Políticas de tempo de buffer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições de rede), você pode definir diferentes políticas de buffering para o player, como alterar a duração mínima para o buffering inicial e para o buffering de reprodução em andamento.

Depois que você chamar `play`, o reprodutor de mídia começa a armazenar o vídeo em buffer. Quando o reprodutor de mídia tiver armazenado em buffer a quantidade de vídeo especificada pelo tempo de buffer inicial, a reprodução será iniciada. Esse processo melhora o tempo de inicialização porque o reprodutor não espera até que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, após os poucos segundos iniciais serem armazenados em buffer, a reprodução começa.

Enquanto o vídeo está sendo renderizado, o TVSDK continua a armazenar em buffer novos fragmentos até que tenha armazenado em buffer a quantidade especificada pelo tempo de buffer de reprodução. Se a duração atual do buffer ficar abaixo do tempo de buffer de reprodução, o reprodutor baixará fragmentos adicionais. Quando a duração atual do buffer estiver acima do tempo de buffer de reprodução em alguns segundos, o TVSDK interromperá o download de fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um longo tempo inicial de buffer antes de iniciar. Isso pode proporcionar uma reprodução suave por mais tempo. No entanto, se as condições da rede forem ruins, a reprodução inicial poderá ser adiada.

Se você habilitar o recurso de ativação instantânea chamando `prepareBuffer`, o buffering inicial começa nesse momento, em vez de esperar por `play`.

## Definir tempos de buffering {#section_05CDD927869D47EBA1D2069B1416B2E4}

A variável `MediaPlayer` O fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o reprodutor de mídia assumirá como padrão 2 segundos para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

1. Configurar o `BufferControlParameters` objeto, que encapsula o tempo de buffer inicial e os parâmetros de controle do tempo de buffer de reprodução.

   Essa classe fornece os seguintes métodos de fábrica:

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
   Se os parâmetros não forem válidos, esses métodos lançarão `MediaPlayerException` com código de erro `PSDKErrorCode.INVALID_ARGUMENT`, como quando as seguintes condições são atendidas:

   * O tempo de buffer inicial é menor que zero.
   * O tempo de buffer inicial é maior que o tempo de buffer.


1. Para definir os valores de parâmetros de buffer, use esta opção `MediaPlayer` método:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obter os valores atuais de parâmetro de buffer, use este `MediaPlayer` método:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Por exemplo, para definir o buffer inicial como 5 segundos e o tempo de buffer de reprodução como 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
