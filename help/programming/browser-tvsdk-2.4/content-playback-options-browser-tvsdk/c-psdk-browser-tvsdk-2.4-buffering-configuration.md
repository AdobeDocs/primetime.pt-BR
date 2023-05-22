---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.
title: Buffering
exl-id: 786379d1-0f2d-44a9-b580-1c8dcbd3fd17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Buffering{#buffering}

Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.

O TVSDK do navegador define um tamanho de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial dentro dele de pelo menos 2 segundos, antes que a mídia comece a ser reproduzida. Depois que o aplicativo chamar `play` mas antes de começar a reprodução, o TVSDK do navegador armazena a mídia em buffer até o momento inicial para fornecer um início suave quando ela realmente começa a ser reproduzida.

## Definir tempos de buffering {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o reprodutor de mídia assumirá como padrão 2 segundos para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

* Para usar os parâmetros de buffer, use o `bufferControlParameters` atributo.

   Por exemplo, para definir o buffer inicial como 2 segundos e o tempo de buffer de reprodução como 30 segundos:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Políticas de tempo de buffer {#section_7EF2947931654CCC8DAB9172391FA4EB}

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições de rede), você pode definir diferentes políticas de buffering para o player, como alterar a duração mínima para o buffering inicial e para o buffering de reprodução em andamento.

Depois que você chamar `play`, o reprodutor de mídia começa a armazenar o vídeo em buffer. Quando o reprodutor de mídia tiver armazenado em buffer a quantidade de vídeo especificada pelo tempo de buffer inicial, a reprodução será iniciada. Esse processo melhora o tempo de inicialização porque o reprodutor não espera até que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, após os poucos segundos iniciais serem armazenados em buffer, a reprodução começa.

Enquanto o vídeo está sendo renderizado, o TVSDK do navegador continua a armazenar em buffer novos fragmentos até que seja armazenada em buffer a quantidade especificada pelo tempo de buffer de reprodução. Se a duração atual do buffer ficar abaixo do tempo de buffer de reprodução, o reprodutor baixará fragmentos adicionais. Quando a duração atual do buffer estiver acima do tempo de buffer de reprodução em alguns segundos, o TVSDK do navegador interromperá o download de fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um longo tempo inicial de buffer antes de iniciar. Isso pode proporcionar uma reprodução suave por mais tempo. No entanto, se as condições da rede forem ruins, a reprodução inicial poderá ser adiada.
