---
description: Em dispositivos que oferecem suporte à aceleração GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar o vídeo no hardware do dispositivo. A disponibilidade do StageVideo depende das versões e dos recursos de diferentes partes do sistema, incluindo Flash Player, hardware de vídeo, SO, drivers, navegador, conexão de rede e contexto de visualização.
title: Recursos e restrições do StageVideo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Visão geral {#stagevideo-capabilities-and-restrictions-overview}

Em dispositivos que oferecem suporte à aceleração GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar o vídeo no hardware do dispositivo. A disponibilidade do StageVideo depende das versões e dos recursos de diferentes partes do sistema, incluindo Flash Player, hardware de vídeo, SO, drivers, navegador, conexão de rede e contexto de visualização.

A variável `StageVideo` A classe permite que você aproveite a aceleração de hardware para apresentar vídeo no mais alto nível de desempenho possível para um dispositivo. A disponibilidade e o desempenho dos `StageVideo` é afetada pelos seguintes fatores:

* **Aceleração de hardware** - Quando a aceleração de hardware estiver disponível, `StageVideo` processa vídeo no hardware do dispositivo. Quando a aceleração de hardware não estiver disponível, a variável `StageVideo` A resposta depende de qual versão do Flash você está executando:

   * *Flash 15 e posterior* - Quando a aceleração de hardware não estiver disponível, `StageVideo` O retorna ao software e você não precisa fazer nada.

     >[!TIP]
     >
     >Quando a aceleração de hardware não estiver disponível, o desempenho poderá ser significativamente reduzido.

   * *Flash 14 e anterior* - Quando a aceleração de hardware não estiver disponível, `StageVideo` fica indisponível. Em um pequeno conjunto de configurações em que a aceleração de hardware não é suportada pelo navegador ou pela GPU, ou está desativada no Flash Player, a exibição de vídeo com a pilha HLS TVSDK falhará. No *HDS* pipeline, você pode alternar de `StageVideo` a uma alternativa, como o objeto Video, que processa o vídeo na CPU.

* **Contexto da apresentação** - Durante a visualização em tela cheia, `StageVideo` O está sempre disponível e o desempenho estará no nível máximo disponível no dispositivo. Quando não estiver visualizando em tela cheia, a apresentação de vídeo se enquadra no contexto do navegador, em que as configurações e os recursos do navegador são usados.

* **wmode** - No contexto do navegador, a variável `wmode` A configuração é essencial para o desempenho. O Adobe recomenda manter `wmode` definir como `direct` para garantir o melhor desempenho possível no contexto do navegador.

  >[!NOTE]
  >
  >A combinação de fatores que incluem `wmode`, `StageVideo`e o Flash resultam em diferentes recursos e restrições, dependendo da velocidade de execução do hardware e da versão do Flash que você está usando.

   * *Flash 15 e posterior* - `StageVideo` está disponível com todos os disponíveis `wmode` configurações. No entanto, se você definir `wmode` para uma configuração diferente de `direct`, o desempenho será menor.

   * *Flash 14 e anterior* - Se você definir `wmode` para uma configuração diferente de `direct`, `StageVideo` não está disponível em todos os navegadores.
