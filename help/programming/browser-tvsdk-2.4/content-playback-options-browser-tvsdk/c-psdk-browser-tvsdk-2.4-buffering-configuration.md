---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.
title: Buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---


# Buffering{#buffering}

Para fornecer uma experiência de visualização mais suave, o TVSDK do navegador às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.

O TVSDK do navegador define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial nesse período, antes que a mídia comece a ser reproduzida, de pelo menos 2 segundos. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK do navegador armazena a mídia em buffer até o momento inicial para fornecer um início suave quando realmente começa a reprodução.

## Definir tempos de buffering {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

O MediaPlayer fornece métodos para definir e obter o tempo de buffering inicial e o tempo de buffering de reprodução.

>[!TIP]
>
>Se você não definir os parâmetros de controle de buffer antes de iniciar a reprodução, o padrão do reprodutor de mídia será 2 segundos para o buffer inicial e 30 segundos para o tempo de buffer de reprodução em andamento.

* Para usar os parâmetros de buffer, use o atributo `bufferControlParameters` do MediaPlayer.

   Por exemplo, para definir o buffer inicial como 2 segundos e o tempo do buffer de reprodução como 30 segundos:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Políticas de tempo de buffer {#section_7EF2947931654CCC8DAB9172391FA4EB}

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições de rede), você pode definir diferentes políticas de buffering para o seu reprodutor, como alterar a duração mínima para buffering inicial e para buffering de reprodução contínua.

Depois de chamar `play`, o reprodutor de mídia inicia o buffer do vídeo. Quando o reprodutor de mídia armazena em buffer a quantidade de vídeo especificada pelo tempo inicial do buffer, a reprodução começa. Esse processo melhora o tempo de inicialização, pois o reprodutor não espera que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, depois que os poucos segundos iniciais são armazenados em buffer, a reprodução começa.

Enquanto o vídeo está sendo renderizado, o TVSDK do navegador continua armazenando novos fragmentos em buffer até que ele tenha colocado em buffer a quantidade especificada pelo tempo do buffer de reprodução. Se o comprimento atual do buffer cair abaixo do tempo do buffer de reprodução, o reprodutor baixará fragmentos adicionais. Depois que o comprimento atual do buffer estiver acima do tempo do buffer de reprodução em alguns segundos, o TVSDK do navegador interromperá o download dos fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um longo tempo inicial de buffering antes de iniciar. Isso pode proporcionar uma reprodução suave por mais tempo; no entanto, se as condições da rede forem precárias, a reprodução inicial poderá ser adiada.

