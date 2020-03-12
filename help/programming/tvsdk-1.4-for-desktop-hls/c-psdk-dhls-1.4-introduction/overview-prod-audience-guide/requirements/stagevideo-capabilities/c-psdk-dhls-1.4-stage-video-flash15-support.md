---
description: Do Flash 15 e posterior, quando a renderização de hardware com o StageVideo não estiver disponível, o StageVideo volta perfeitamente para um objeto StageVideo de software.
seo-description: Do Flash 15 e posterior, quando a renderização de hardware com o StageVideo não estiver disponível, o StageVideo volta perfeitamente para um objeto StageVideo de software.
seo-title: Suporte a Flash 15 para StageVideo
title: Suporte a Flash 15 para StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Suporte a Flash 15 para StageVideo{#flash-support-for-stagevideo}

Do Flash 15 e posterior, quando a renderização de hardware com o StageVideo não estiver disponível, o StageVideo volta perfeitamente para um objeto StageVideo de software.

Considere as seguintes informações sobre o fallback do Flash 15 StageVideo para software:

* Nenhuma alteração de código é necessária em seu aplicativo.
* Nenhuma alteração no TVSDK é necessária.

   Você não precisa de uma atualização do TVSDK para usar o fallback do StageVideo para o software.
* Seus aplicativos precisam ser recompilados para Flash 15.
* Os aplicativos que você recompila para Flash 15 continuarão funcionando com o Flash 14 e versões anteriores, desde que esses aplicativos não usem novas APIs introduzidas no Flash Player 15.

   Se seu aplicativo Flash 14 precisar usar uma nova API Flash 15, você deverá chamar dinamicamente a API com uma conversão para o tipo de objeto, para que o aplicativo não falhe no Flash Player 14 no tempo de execução.

## Sobreposições HTML {#html-overlays}

No Flash 15 e posterior, você pode manter uma exibição contínua de sobreposições HTML quando o hardware StageVideo não estiver disponível e voltar para o software StageVideo. Para ativar este recurso, defina `wmode=opaque`.

Alguns navegadores mais antigos não suportam aceleração de hardware. Para obter mais informações sobre esses requisitos, consulte os requisitos [mínimos do](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)StageVideo. Quando você define `wmode=opaque`, o vídeo é renderizado com o software StageVideo, que pode afetar o desempenho. Normalmente, a configuração renderiza `wmode=direct` diretamente o vídeo para a GPU, o que resulta em um desempenho muito melhor. No entanto, essa opção também substitui sobreposições HTML.
