---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.
title: Políticas de tempo de buffer
exl-id: 78f1bb9f-3d10-4f05-90dd-5b52eee0feec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Políticas de tempo de buffer {#buffering-time-policies}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.

O TVSDK define um tamanho de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial de pelo menos 5 segundos antes de a mídia começar a ser reproduzida. Depois que o aplicativo chamar `play` mas antes de começar a reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para dar um início suave quando ela realmente começa a ser reproduzida.

Você pode alterar os tempos de buffer definindo novas políticas de buffering.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições de rede), você pode definir diferentes políticas de buffering para o player, como alterar a duração mínima para o buffering inicial e para o buffering de reprodução em andamento.

Depois que você chamar `play`, o reprodutor de mídia começa a armazenar o vídeo em buffer. Quando o reprodutor de mídia tiver armazenado em buffer a quantidade de vídeo especificada pelo tempo de buffer inicial, a reprodução será iniciada. Esse processo melhora o tempo de inicialização porque o reprodutor não espera até que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, após os poucos segundos iniciais serem armazenados em buffer, a reprodução começa.

Enquanto o vídeo está sendo renderizado, o TVSDK continua a armazenar em buffer novos fragmentos até que tenha armazenado em buffer a quantidade especificada pelo tempo de buffer de reprodução. Se a duração atual do buffer ficar abaixo do tempo de buffer de reprodução, o reprodutor baixará fragmentos adicionais. Quando a duração atual do buffer estiver acima do tempo de buffer de reprodução em alguns segundos, o TVSDK interromperá o download de fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um longo tempo inicial de buffer antes de iniciar. Isso pode proporcionar uma reprodução suave por mais tempo. No entanto, se as condições da rede forem ruins, a reprodução inicial poderá ser adiada.
