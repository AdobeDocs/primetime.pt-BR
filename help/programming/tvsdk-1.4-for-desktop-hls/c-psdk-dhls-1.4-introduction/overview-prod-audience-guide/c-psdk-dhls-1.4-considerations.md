---
description: Para usar o TVSDK com mais eficiência, você deve considerar determinados detalhes de sua operação e seguir determinadas práticas recomendadas.
title: Considerações e práticas recomendadas
exl-id: 5e1e09e1-f22e-4797-807a-14dbf50bb835
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK com mais eficiência, você deve considerar determinados detalhes de sua operação e seguir determinadas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar o TVSDK:

* O Adobe Primetime não funciona em emuladores ou simuladores.

   Você deve usar dispositivos reais para testes.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado, em que os fluxos de vídeo e áudio estão na mesma representação, ou não multiplexado, em que os fluxos de vídeo e áudio estão em representações separadas.
* A API TVSDK é implementada no ActionScript.
* A reprodução de vídeo requer o Adobe Video Engine (AVE). Isso afeta como e quando os recursos de mídia podem ser acessados:

   * As legendas ocultas são compatíveis na medida em que forem fornecidas pelo AVE.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento do progresso da reprodução do fluxo para o gerenciamento de anúncios e o Video Analytics deve usar o tempo de reprodução real, de modo que os relatórios e o comportamento da interface do usuário podem não rastrear com precisão a mídia e o conteúdo do anúncio.
   * O nome do agente do usuário de entrada para todas as solicitações HTTP do TVSDK nesta plataforma é atribuído ao seguinte padrão de cadeia de caracteres:

      ```
      "Adobe Flash Player"
      ```

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para o TVSDK:

* Use o HLS versão 3.0 ou superior para o conteúdo do programa.
* Para TVSDK 1.4 para DHLS, o carregamento lento de anúncios é habilitado por padrão.

   Para conteúdo sem antes da exibição ou no meio da exibição, é possível usar `AdvertisingMetadata.delayAdLoading` para acelerar ainda mais o carregamento de conteúdo.
