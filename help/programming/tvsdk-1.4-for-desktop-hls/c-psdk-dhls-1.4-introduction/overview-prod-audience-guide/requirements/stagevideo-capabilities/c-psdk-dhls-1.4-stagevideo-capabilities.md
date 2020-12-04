---
description: Em dispositivos que suportam aceleração de GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo no hardware do dispositivo. A disponibilidade do StageVideo depende das versões e dos recursos de diferentes partes do seu sistema, incluindo Flash Player, hardware de vídeo, SO, drivers, navegador, conexão de rede e contexto de exibição.
seo-description: Em dispositivos que suportam aceleração de GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo no hardware do dispositivo. A disponibilidade do StageVideo depende das versões e dos recursos de diferentes partes do seu sistema, incluindo Flash Player, hardware de vídeo, SO, drivers, navegador, conexão de rede e contexto de exibição.
seo-title: Recursos e restrições do StageVideo
title: Recursos e restrições do StageVideo
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Visão geral {#stagevideo-capabilities-and-restrictions-overview}

Em dispositivos que suportam aceleração de GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo no hardware do dispositivo. A disponibilidade do StageVideo depende das versões e dos recursos de diferentes partes do seu sistema, incluindo Flash Player, hardware de vídeo, SO, drivers, navegador, conexão de rede e contexto de exibição.

A classe `StageVideo` permite que você aproveite a aceleração de hardware para apresentar vídeo no mais alto nível de desempenho possível para um dispositivo. A disponibilidade e o desempenho de `StageVideo` são afetados pelos seguintes fatores:

* **Aceleração**  de hardware - Quando a aceleração de hardware está disponível,  `StageVideo` processa o vídeo no hardware do dispositivo. Quando a aceleração de hardware não estiver disponível, as respostas `StageVideo` dependerão da versão do Flash que você estiver executando:

   * *Flash 15 e posterior*  - Quando a aceleração de hardware não está disponível,  `StageVideo` volta para o software e você não precisa fazer nada.

      >[!TIP]
      >
      >Quando a aceleração do hardware não está disponível, o desempenho pode diminuir significativamente.

   * *Flash 14 e anterior*  - Quando a aceleração de hardware não está disponível,  `StageVideo` ela fica indisponível. Em um pequeno conjunto de configurações em que a aceleração de hardware não é suportada pelo navegador ou pela GPU, ou está desativada no Flash Player, a exibição de vídeo com a pilha HLS TVSDK falhará. No pipeline *HDS*, você pode alternar de `StageVideo` para um alternativo, como o objeto Video, que processa vídeo na CPU.

* **Contexto**  da apresentação - Durante a visualização em tela cheia,  `StageVideo` está sempre disponível e o desempenho estará no nível máximo disponível no dispositivo. Quando não estiver exibindo tela cheia, a apresentação de vídeo se enquadra no contexto do navegador, onde as configurações e os recursos do navegador são usados.

* **wmode**  - No contexto do navegador, a  `wmode` configuração é essencial para o desempenho. O Adobe recomenda manter `wmode` definido como `direct` para garantir o melhor desempenho possível no contexto do navegador.

   >[!NOTE]
   >
   >A combinação de fatores que incluem `wmode`, `StageVideo` e Flash resulta em diferentes recursos e restrições, dependendo da velocidade de execução do hardware e da versão do Flash que você está usando.

   * *Flash 15 e posterior*  -  `StageVideo` está disponível com todas as  `wmode` configurações disponíveis. No entanto, se você definir `wmode` para uma configuração diferente de `direct`, o desempenho será menor.

   * *Flash 14 e anterior*  - se você definir  `wmode` para uma configuração diferente  `direct`, não  `StageVideo` estará disponível em todos os navegadores.

