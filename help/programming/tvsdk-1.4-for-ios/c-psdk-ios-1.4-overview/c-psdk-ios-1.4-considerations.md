---
description: Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.
seo-description: Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.
seo-title: Considerações e práticas recomendadas
title: Considerações e práticas recomendadas
uuid: b37a5710-e811-4c3e-be8c-7c34ee5944e5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK de forma mais eficiente, considere alguns detalhes de sua operação e siga certas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar o TVSDK:

* O Adobe Primetime não funciona em simuladores iOS.

   Você deve usar dispositivos reais para teste.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado, onde os fluxos de vídeo e áudio estão na mesma execução, ou não multiplexados, onde os fluxos de vídeo e áudio estão em representações separadas.
* A API TVSDK é implementada em Objetive-C.
* A reprodução de vídeo requer a estrutura nativa da Apple AV Foundation. Isso afeta como e quando os recursos de mídia, incluindo legendas fechadas e linhas do tempo, podem ser acessados:

   * Os ajustes da linha do tempo não podem ser revisados após a configuração inicial.

      Por exemplo, um anúncio não pode ser removido da linha do tempo depois de ser reproduzido. Se o usuário retornar à apresentação, o mesmo anúncio será reproduzido novamente mesmo se a política tiver sido remover o anúncio.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações que são registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar entre a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento de andamento da reprodução de fluxo para o gerenciamento de anúncios e o Video Analytics deve usar o tempo de reprodução real, de modo que o comportamento de relatório e interface do usuário pode não rastrear com precisão o conteúdo de mídia e anúncio.
   * O agente de usuário recebido para todas as solicitações HTTP do TVSDK nesta plataforma é determinado pelo dispositivo e pela versão do iOS que está sendo executada no dispositivo.

      O valor da sequência do agente do usuário padroniza o que o sistema operacional atribui.

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para o TVSDK:

* Use a versão 3.0 ou superior do HLS para conteúdo do programa.
* Use a ferramenta mediastreamvalidator da Apple para validar fluxos VOD.
* A `PTSDKConfig` classe fornece métodos para aplicar o SSL em solicitações feitas aos servidores de decisão de anúncio Primetime, DRM e Video Analytics.

   Para obter mais informações, consulte os métodos `forceHTTPS` e `isForcingHTTPS` nesta classe.

   >[!IMPORTANT]
   >
   >As solicitações para domínios de terceiros, como pixels de rastreamento de anúncios, URLs de conteúdo e anúncios, e solicitações semelhantes não são modificadas. É responsabilidade dos provedores de conteúdo e servidores de publicidade fornecer URLs compatíveis com HTTPS.

