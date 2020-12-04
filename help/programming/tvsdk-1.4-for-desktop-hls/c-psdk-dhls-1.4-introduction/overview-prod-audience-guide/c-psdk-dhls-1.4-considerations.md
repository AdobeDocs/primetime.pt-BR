---
description: Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.
seo-description: Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.
seo-title: Considerações e práticas recomendadas
title: Considerações e práticas recomendadas
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar o TVSDK:

* A Adobe Primetime não funciona em emuladores ou simuladores.

   Você deve usar dispositivos reais para teste.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado, onde os fluxos de vídeo e áudio estão na mesma execução, ou não multiplexados, onde os fluxos de vídeo e áudio estão em representações separadas.
* A API TVSDK é implementada no ActionScript.
* A reprodução de vídeo requer o Adobe Video Engine (AVE). Isso afeta como e quando os recursos de mídia podem ser acessados:

   * As legendas ocultas são suportadas na medida fornecida pelo AVE.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações que são registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar entre a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento de andamento da reprodução de fluxo para o gerenciamento de anúncios e o Video Analytics deve usar o tempo de reprodução real, de modo que o comportamento do relatórios e da interface do usuário pode não rastrear com precisão o conteúdo de mídia e anúncio.
   * O nome do agente de usuário recebido para todas as solicitações HTTP do TVSDK nesta plataforma recebe o seguinte padrão de string:

      ```
      "Adobe Flash Player"
      ```

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para o TVSDK:

* Use a versão 3.0 ou superior do HLS para conteúdo de programas.
* Para TVSDK 1.4 para DHLS, o carregamento lento de anúncio é ativado por padrão.

   Para conteúdo sem precedente ou intermediário, você pode usar `AdvertisingMetadata.delayAdLoading` para acelerar ainda mais o carregamento do conteúdo.

