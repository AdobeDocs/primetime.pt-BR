---
description: Para usar o TVSDK de maneira mais eficaz, considere alguns detalhes de sua operação e siga determinadas práticas recomendadas.
title: Considerações e práticas recomendadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Considerações e práticas recomendadas {#considerations-and-best-practices}

Para usar o TVSDK de maneira mais eficaz, considere alguns detalhes de sua operação e siga determinadas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar TVSDK:

* A API TVSDK é implementada em Java.
* No momento, o Adobe Primetime não funciona em emuladores Android.

   Você deve usar dispositivos reais para testes.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado (fluxos de vídeo e áudio na mesma representação) ou não multiplexado (fluxos de vídeo e áudio em representações separadas).
* Atualmente, é necessário executar a maioria das operações da API TVSDK no thread da interface do usuário, que é o thread principal do Android.

   As operações executadas corretamente no thread principal podem gerar um erro e sair quando executadas em um thread em segundo plano.
* A reprodução de vídeo requer o Adobe Video Engine (AVE). Isso afeta como e quando os recursos de mídia podem ser acessados:

   * As legendas ocultas são suportadas na extensão fornecida pelo AVE.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar entre a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento do progresso da reprodução de fluxo para o gerenciamento de anúncios e o Video Analytics devem usar o tempo de reprodução real, de modo que os relatórios e o comportamento da interface do usuário podem não rastrear precisamente o conteúdo de mídia e anúncio.
   * O seguinte padrão de sequência é atribuído ao nome do agente de usuário de entrada para todas as solicitações de mídia do TVSDK nesta plataforma:

      ```
      "Adobe Primetime/" + originalUserAgent
      ```

      Todas as chamadas relacionadas a anúncios usam o agente de usuário padrão do Android ou o agente de usuário personalizado, se você configurá-lo ao configurar os metadados de inserção de anúncio.

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para TVSDK:

* Use a versão 3.0 ou superior do HLS para conteúdo do programa.
* Execute a maioria das operações do TVSDK no thread principal (interface do usuário), não em threads em segundo plano.
* Para TVSDK 3.0 para Android, a resolução de anúncio lento é ativada por padrão.

Para conteúdo sem precedente ou intermediário, você pode usar `AdvertisingMetadata.setPreroll(false)` para acelerar o carregamento do conteúdo.