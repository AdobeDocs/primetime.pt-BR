---
description: A partir do Flash 15 e posterior, quando a renderização de hardware com o StageVideo não estiver disponível, o StageVideo retorna perfeitamente a um objeto StageVideo de software.
title: Suporte do Flash 15 para StageVideo
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Suporte do Flash 15 para StageVideo{#flash-support-for-stagevideo}

A partir do Flash 15 e posterior, quando a renderização de hardware com o StageVideo não estiver disponível, o StageVideo retorna perfeitamente a um objeto StageVideo de software.

Considere as seguintes informações sobre o fallback StageVideo do Flash 15 para o software:

* Não são necessárias alterações de código em seu aplicativo.
* Não é necessária nenhuma alteração no TVSDK.

   Você não precisa de uma atualização do TVSDK para usar o fallback StageVideo para o software.
* Seus aplicativos precisam ser recompilados para o Flash 15.
* Os aplicativos recompilados para o Flash 15 continuarão a funcionar com o Flash 14 e versões anteriores, desde que esses aplicativos não usem novas APIs introduzidas no Flash Player 15.

   Se o aplicativo do Flash 14 precisar usar uma nova API do Flash 15, você deverá chamar dinamicamente a API com uma conversão para o Object type, para que o aplicativo não falhe no Flash Player 14 no tempo de execução.

## Sobreposições de HTML {#html-overlays}

No Flash 15 e mais recente, você pode manter uma exibição perfeita das sobreposições de HTML quando o hardware StageVideo se tornar indisponível e voltar para o software StageVideo. Para ativar esse recurso, defina `wmode=opaque`.

Alguns navegadores mais antigos não suportam aceleração de hardware. Para obter mais informações sobre esses requisitos, consulte [Requisitos mínimos do StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Ao definir `wmode=opaque`, o vídeo é renderizado com o software StageVideo, que pode afetar o desempenho. Normalmente, a configuração `wmode=direct` renderiza vídeo diretamente para a GPU, o que resulta em um desempenho muito melhor. No entanto, essa opção também substitui as sobreposições de HTML.
