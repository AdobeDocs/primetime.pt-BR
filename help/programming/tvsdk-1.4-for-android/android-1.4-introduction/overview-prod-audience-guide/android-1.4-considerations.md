---
description: Para usar o TVSDK com mais eficiência, você deve considerar determinados detalhes de sua operação e seguir determinadas práticas recomendadas.
title: Considerações e práticas recomendadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK com mais eficiência, você deve considerar determinados detalhes de sua operação e seguir determinadas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar o TVSDK:

* No momento, o Adobe Primetime não funciona em emuladores de Android.

  Você deve usar dispositivos reais para testes.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado, em que os fluxos de vídeo e áudio estão na mesma representação, ou não multiplexado, em que os fluxos de vídeo e áudio estão em representações separadas.
* A API do TVSDK é implementada em Java.
* Atualmente, é necessário executar a maioria das operações da API TVSDK no thread da interface do usuário, que é o principal thread do Android.

  As operações executadas corretamente na thread principal podem gerar um erro e sair ao serem executadas em uma thread em segundo plano.
* A reprodução de vídeo requer o Adobe Video Engine (AVE). Isso afeta como e quando os recursos de mídia podem ser acessados:

   * As legendas ocultas são compatíveis na medida em que forem fornecidas pelo AVE.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações registradas no manifesto do recurso de fluxo.

     Não há uma maneira confiável de ressincronizar a linha do tempo virtual ideal com a linha do tempo de reprodução real. O rastreamento do progresso da reprodução do fluxo para o gerenciamento de anúncios e o Video Analytics deve usar o tempo de reprodução real, de modo que os relatórios e o comportamento da interface do usuário podem não rastrear com precisão a mídia e o conteúdo do anúncio.
   * O nome do agente do usuário de entrada para todas as solicitações de mídia do TVSDK nesta plataforma é atribuído ao seguinte padrão de sequência:

     ```
     "Adobe Primetime/ + 
     <varname>
     originalUserAgent
     </varname>" 
     ```

     Todas as chamadas relacionadas a anúncios usam o agente de usuário padrão do Android ou o agente de usuário personalizado se você configurá-lo ao configurar metadados de inserção de anúncios.

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para o TVSDK:

* Use o HLS versão 3.0 ou superior para o conteúdo do programa.
* Execute a maioria das operações TVSDK na thread principal (interface do usuário), não em threads em segundo plano.
