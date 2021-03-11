---
description: Para usar o TVSDK de maneira mais eficaz, considere alguns detalhes de sua operação e siga determinadas práticas recomendadas.
title: Considerações e práticas recomendadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Considerações e práticas recomendadas {#considerations-and-best-practices}

Para usar o TVSDK de maneira mais eficaz, considere alguns detalhes de sua operação e siga determinadas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar TVSDK:

* O Adobe Primetime não funciona em simuladores do iOS.

   Você deve usar dispositivos reais para testes.

* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).

* O conteúdo do vídeo principal pode ser multiplexado, onde os fluxos de vídeo e áudio estão na mesma representação, ou não multiplexados, onde os fluxos de vídeo e áudio estão em representações separadas.

* A API TVSDK é implementada em Objetive-C.

* A reprodução de vídeo requer a estrutura nativa da Apple AV Foundation. Isso afeta como e quando os recursos de mídia, incluindo legendas ocultas e linhas do tempo, podem ser acessados:

   * Os ajustes da linha do tempo não podem ser revisados após a configuração inicial.

      Por exemplo, um anúncio não pode ser removido da linha do tempo depois de ser reproduzido. Se o usuário retornar à apresentação, o mesmo anúncio será reproduzido novamente mesmo que a política tenha sido a remoção do anúncio.

   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar entre a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento do progresso da reprodução de fluxo para o gerenciamento de anúncios e o Video Analytics devem usar o tempo de reprodução real, de modo que os relatórios e o comportamento da interface do usuário podem não rastrear precisamente o conteúdo de mídia e anúncio.

   * O agente de usuário de entrada para todas as solicitações HTTP do TVSDK nessa plataforma é determinado pelo dispositivo e pela versão do iOS que está sendo executada no dispositivo.

      O valor da string do agente do usuário assume como padrão o que o sistema operacional atribui.

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para TVSDK:

* Use a versão 3.0 ou superior do HLS para conteúdo do programa.

* Use a ferramenta mediastreamvalidator da Apple para validar fluxos VOD.

* A classe PTSDKConfig fornece métodos para aplicar o SSL em solicitações feitas aos servidores de decisão de anúncio do Primetime, DRM e Video Analytics.

Para obter mais informações, consulte os métodos forceHTTPS e isForcingHTTPS nesta classe.

>[!IMPORTANT]
>
>As solicitações para domínios de terceiros, como pixels de rastreamento de anúncios, URLs de conteúdo e anúncios, e solicitações semelhantes não são modificadas. É de responsabilidade dos provedores de conteúdo e servidores de anúncios fornecer URLs compatíveis com HTTPS.
