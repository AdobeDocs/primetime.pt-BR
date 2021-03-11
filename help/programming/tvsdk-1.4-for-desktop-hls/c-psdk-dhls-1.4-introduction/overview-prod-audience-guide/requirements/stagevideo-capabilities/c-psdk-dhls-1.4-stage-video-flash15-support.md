---
description: A partir do Flash 15 e posterior, quando a renderização de hardware com StageVideo não está disponível, o StageVideo volta sem interrupções para um objeto de software StageVideo.
title: Suporte ao Flash 15 para StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Suporte ao Flash 15 para StageVideo{#flash-support-for-stagevideo}

A partir do Flash 15 e posterior, quando a renderização de hardware com StageVideo não está disponível, o StageVideo volta sem interrupções para um objeto de software StageVideo.

Considere as seguintes informações sobre a fallback do Flash 15 StageVideo para software:

* Nenhuma alteração de código é necessária em seu aplicativo.
* Nenhuma alteração no TVSDK é necessária.

   Você não precisa de uma atualização do TVSDK para usar a fallback do StageVideo no software.
* Seus aplicativos precisam ser recompilados para o Flash 15.
* Os aplicativos que você recompila para o Flash 15 continuarão a funcionar com o Flash 14 e versões anteriores, desde que esses aplicativos não usem novas APIs introduzidas no Flash Player 15.

   Se o aplicativo Flash 14 precisar usar uma nova API Flash 15, você deve chamar dinamicamente a API com uma conversão para o tipo Object , para que o aplicativo não falhe no Flash Player 14 no tempo de execução.

## Sobreposições HTML {#html-overlays}

No Flash 15 e posterior, você pode manter uma exibição contínua de sobreposições HTML quando o hardware StageVideo se tornar indisponível e voltar para o software StageVideo. Para habilitar esse recurso, defina `wmode=opaque`.

Alguns navegadores mais antigos não suportam aceleração de hardware. Para obter mais informações sobre esses requisitos, consulte [Requisitos mínimos do StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Ao definir `wmode=opaque`, o vídeo é renderizado com o software StageVideo, o que pode afetar o desempenho. Normalmente, definir `wmode=direct` renderiza diretamente o vídeo para a GPU, o que resulta em um desempenho muito melhor. No entanto, essa opção também substitui as sobreposições HTML.
