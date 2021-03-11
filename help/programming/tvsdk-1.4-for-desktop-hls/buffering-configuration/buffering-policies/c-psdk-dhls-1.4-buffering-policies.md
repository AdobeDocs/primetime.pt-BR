---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.
title: Políticas de tempo de buffer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Políticas de tempo de buffer {#buffering-time-policies}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o reprodutor é armazenado em buffer.

O TVSDK define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial de pelo menos 5 segundos durante a reprodução da mídia. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para fornecer um início suave quando realmente começa a reproduzir.

Você pode alterar os tempos do buffer definindo novas políticas de buffer.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições de rede), você pode definir diferentes políticas de buffering para o seu reprodutor, como alterar a duração mínima para buffering inicial e para buffering de reprodução contínua.

Depois de chamar `play`, o reprodutor de mídia inicia o buffer do vídeo. Quando o reprodutor de mídia armazena em buffer a quantidade de vídeo especificada pelo tempo inicial do buffer, a reprodução começa. Esse processo melhora o tempo de inicialização, pois o reprodutor não espera que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, depois que os poucos segundos iniciais são armazenados em buffer, a reprodução começa.

Enquanto o vídeo é renderizado, o TVSDK continua armazenando novos fragmentos em buffer até que ele tenha colocado em buffer a quantidade especificada pelo tempo do buffer de reprodução. Se o comprimento atual do buffer cair abaixo do tempo do buffer de reprodução, o reprodutor baixará fragmentos adicionais. Depois que o comprimento atual do buffer estiver acima do tempo do buffer de reprodução em alguns segundos, o TVSDK interromperá o download dos fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um longo tempo inicial de buffering antes de iniciar. Isso pode proporcionar uma reprodução suave por mais tempo; no entanto, se as condições da rede forem precárias, a reprodução inicial poderá ser adiada.

