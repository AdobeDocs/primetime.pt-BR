---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.
seo-description: Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.
seo-title: Buffering
title: Buffering
uuid: 9937731d-013e-41e9-a4c9-f7a54a5e654d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Buffering{#buffering}

Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.

O TVSDK do navegador define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial de pelo menos 2 segundos antes da reprodução da mídia. Depois que o aplicativo chama, `play` mas antes do início da reprodução, o TVSDK do navegador armazena a mídia em buffer até o momento inicial para proporcionar uma inicialização suave quando a reprodução é iniciada.

## Definir tempos de buffering {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering da reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o player de mídia assumirá 2 segundos como padrão para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

* Para usar os parâmetros de buffer, use o `bufferControlParameters` atributo MediaPlayer.

   Por exemplo, para definir o buffer inicial para 2 segundos e o tempo do buffer de reprodução para 30 segundos:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Políticas de tempo de buffer {#section_7EF2947931654CCC8DAB9172391FA4EB}

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições da rede), você pode definir diferentes políticas de buffering para o player, como alterar a duração mínima para buffering inicial e para buffering contínuo de reprodução.

Depois de ligar `play`, o player de mídia inicia o buffering do vídeo. Quando o player de mídia armazena em buffer a quantidade de vídeo especificada pelo tempo inicial do buffer, a reprodução é iniciada. Esse processo melhora o tempo de inicialização porque o player não espera que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, após os poucos segundos iniciais serem armazenados em buffer, a reprodução é iniciada.

Enquanto o vídeo está sendo renderizado, o TVSDK do navegador continua a armazenar em buffer novos fragmentos até que ele tenha armazenado em buffer a quantidade especificada pelo tempo do buffer de reprodução. Se o tamanho atual do buffer cair abaixo do tempo de buffer de reprodução, o player baixará fragmentos adicionais. Quando a duração atual do buffer estiver acima do tempo do buffer de reprodução em alguns segundos, o TVSDK do navegador interromperá o download dos fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um tempo de buffering inicial longo antes de iniciar. Isso pode propiciar uma reprodução suave por mais tempo. no entanto, se as condições da rede forem precárias, a reprodução inicial poderá ser atrasada.

