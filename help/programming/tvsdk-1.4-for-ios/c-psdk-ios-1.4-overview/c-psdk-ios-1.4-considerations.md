---
description: Para usar o TVSDK com mais eficiência, você deve considerar determinados detalhes de sua operação e seguir determinadas práticas recomendadas.
title: Considerações e práticas recomendadas
exl-id: d10532a5-bf96-4233-86f1-b135f6e1c0f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Considerações e práticas recomendadas{#considerations-and-best-practices}

Para usar o TVSDK com mais eficiência, você deve considerar determinados detalhes de sua operação e seguir determinadas práticas recomendadas.

## Considerações {#section_tvsdk_considerations}

Lembre-se das seguintes informações ao usar o TVSDK:

* O Adobe Primetime não funciona em simuladores do iOS.

   Você deve usar dispositivos reais para testes.
* A reprodução é compatível somente com conteúdo HTTP Live Streaming (HLS).
* O conteúdo de vídeo principal pode ser multiplexado, em que os fluxos de vídeo e áudio estão na mesma representação, ou não multiplexado, em que os fluxos de vídeo e áudio estão em representações separadas.
* A API do TVSDK é implementada no Objetive-C.
* A reprodução de vídeo requer a estrutura nativa Apple AV Foundation. Isso afeta como e quando os recursos de mídia, incluindo legendas ocultas e linhas do tempo, podem ser acessados:

   * Os ajustes de linha do tempo não podem ser revisados após a configuração inicial.

      Por exemplo, um anúncio não pode ser removido da linha do tempo depois de ser reproduzido. Se o usuário buscar de volta na apresentação, o mesmo anúncio será reproduzido novamente mesmo se a política tiver sido a remoção do anúncio.
   * Dependendo da precisão do codificador, a duração real da mídia codificada pode diferir das durações registradas no manifesto do recurso de fluxo.

      Não há uma maneira confiável de ressincronizar a linha do tempo virtual ideal e a linha do tempo de reprodução real. O rastreamento do progresso da reprodução do fluxo para o gerenciamento de anúncios e o Video Analytics deve usar o tempo de reprodução real, de modo que os relatórios e o comportamento da interface do usuário podem não rastrear com precisão a mídia e o conteúdo do anúncio.
   * O agente do usuário de entrada para todas as solicitações HTTP do TVSDK nesta plataforma é determinado pelo dispositivo e pela versão do iOS em execução no dispositivo.

      O valor da sequência de agente do usuário é padronizado para o que o sistema operacional atribui.

## Práticas recomendadas {#section_tvsdk_best_practices}

Estas são as práticas recomendadas para o TVSDK:

* Use o HLS versão 3.0 ou superior para o conteúdo do programa.
* Use a ferramenta mediastreamvalidator do Apple para validar fluxos de VOD.
* A variável `PTSDKConfig` A classe fornece métodos para impor o SSL em solicitações feitas aos servidores do Primetime ad decisioning, DRM e Video Analytics.

   Para obter mais informações, consulte `forceHTTPS` e `isForcingHTTPS` nesta classe.

   >[!IMPORTANT]
   >
   >As solicitações para domínios de terceiros, como pixels de rastreamento de anúncios, URLs de conteúdo e anúncios e solicitações semelhantes, não são modificadas. É de responsabilidade dos provedores de conteúdo e servidores de anúncios fornecer URLs compatíveis com HTTPS.
