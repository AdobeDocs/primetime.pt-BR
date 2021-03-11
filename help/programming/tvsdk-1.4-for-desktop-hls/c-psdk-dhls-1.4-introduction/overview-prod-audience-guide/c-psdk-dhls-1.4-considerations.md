---
description: Para usar o TVSDK de maneira mais eficaz, considere alguns detalhes de sua operação e siga determinadas práticas recomendadas.
title: Considerações e práticas recomendadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK de maneira mais eficaz, considere alguns detalhes de sua operação e siga determinadas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar TVSDK:

* O Adobe Primetime não funciona em emuladores ou simuladores.

   Você deve usar dispositivos reais para testes.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo do vídeo principal pode ser multiplexado, onde os fluxos de vídeo e áudio estão na mesma representação, ou não multiplexados, onde os fluxos de vídeo e áudio estão em representações separadas.
* A API TVSDK é implementada no ActionScript.
* A reprodução de vídeo requer o Adobe Video Engine (AVE). Isso afeta como e quando os recursos de mídia podem ser acessados:

   * As legendas ocultas são suportadas na extensão fornecida pelo AVE.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar entre a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento do progresso da reprodução de fluxo para o gerenciamento de anúncios e o Video Analytics devem usar o tempo de reprodução real, de modo que os relatórios e o comportamento da interface do usuário podem não rastrear precisamente o conteúdo de mídia e anúncio.
   * O nome do agente de usuário de entrada para todas as solicitações HTTP do TVSDK nesta plataforma recebe o seguinte padrão de sequência de caracteres:

      ```
      "Adobe Flash Player"
      ```

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para TVSDK:

* Use a versão 3.0 ou superior do HLS para conteúdo do programa.
* Para TVSDK 1.4 para DHLS, o carregamento lento de anúncio é ativado por padrão.

   Para conteúdo sem precedente ou intermediário, você pode usar `AdvertisingMetadata.delayAdLoading` para acelerar ainda mais o carregamento do conteúdo.

