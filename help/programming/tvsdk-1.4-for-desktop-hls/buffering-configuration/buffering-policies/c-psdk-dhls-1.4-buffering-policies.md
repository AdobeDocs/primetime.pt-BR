---
description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.
seo-description: Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.
seo-title: Políticas de tempo de buffer
title: Políticas de tempo de buffer
uuid: 8d3ce9be-cca4-485e-ba66-d2f2aa6822dd
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Políticas de tempo de buffer {#buffering-time-policies}

Para fornecer uma experiência de visualização mais suave, o TVSDK às vezes armazena o fluxo de vídeo em buffer. Você pode configurar o modo como o player armazena em buffer.

O TVSDK define uma duração de buffer de reprodução de pelo menos 30 segundos e um tempo de buffer inicial de pelo menos 5 segundos antes da reprodução dos start de mídia. Depois que o aplicativo chama `play`, mas antes do início da reprodução, o TVSDK armazena a mídia em buffer até o momento inicial para fornecer um start suave quando ela é realmente start.

Você pode alterar os tempos do buffer definindo novas políticas de buffering.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Dependendo do seu ambiente (incluindo o dispositivo, o sistema operacional ou as condições da rede), você pode definir diferentes políticas de buffering para o player, como alterar a duração mínima para buffering inicial e para buffering contínuo de reprodução.

Depois que você chamar `play`, o player de mídia começará a armazenar o vídeo em buffer. Quando o player de mídia armazena em buffer a quantidade de vídeo especificada pelo tempo inicial do buffer, a reprodução é iniciada. Esse processo melhora o tempo de start porque o player não espera que todo o buffer de reprodução seja preenchido antes de iniciar a reprodução. Em vez disso, após os poucos segundos iniciais serem armazenados em buffer, a reprodução é iniciada.

Enquanto o vídeo está sendo renderizado, o TVSDK continua a armazenar em buffer novos fragmentos até que ele tenha armazenado em buffer a quantidade especificada pelo tempo do buffer de reprodução. Se o tamanho atual do buffer cair abaixo do tempo de buffer de reprodução, o player baixará fragmentos adicionais. Quando a duração atual do buffer estiver acima do tempo do buffer de reprodução em alguns segundos, o TVSDK interromperá o download dos fragmentos.

>[!TIP]
>
>Se o valor inicial do buffer for alto, ele pode dar ao usuário um tempo de buffering inicial longo antes de iniciar. Isso pode propiciar uma reprodução suave por mais tempo. no entanto, se as condições da rede forem precárias, a reprodução inicial poderá ser atrasada.

