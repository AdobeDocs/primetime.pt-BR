---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Ajuda do Primetime Ad Insertion
user-guide-description: Explica como monetizar o conteúdo inserindo anúncios dinâmicos direcionados ao usuário no servidor e engajar o público-alvo com anúncios personalizados.
translation-type: tm+mt
source-git-commit: fac84687085f289e984c189665bfe775337592b3
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 9%

---


# Primetime Ad Insertion Help {#ad-insertion}

+ [Visão geral do Primetime Ad Insertion](home.md)
+ Introdução ao Primetime Ad Insertion{#get-started}
   + [Visão geral](get-started-ptai.md)
   + [Preparar para utilizar Primetime Ad Insertion](setup-ptai.md)
   + [Integrar seu servidor de publicidade](integrate-ad-server.md)
   + [Integrar seu CDN](integrate-cdn.md)
   + [Usar inserção de anúncio em fluxos ao vivo/lineares](ad-insertion-live-linear-stream.md)
   + [Usar inserção de anúncio para VOD](ad-insertion-vod.md)
   + [Configurar o rastreamento de anúncios](set-up-ad-tracking.md)
+ [Notas de versão do Primetime Ad Insertion](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [Ferramenta de depuração do servidor manifest](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ API do servidor manifest para Ad Insertion {#manifest-server}
   + [Visão geral das interações do servidor manifest](msapi-topics/ms-overview.md)
   + Introdução ao Manifest Server {#get-started}
      + [Enviar um comando para o servidor de manifesto](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [Parâmetros do query do servidor manifest](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + Solicitações de inserção de anúncio {#ad-insert}
      + [Solicitações de inserção de anúncio](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [Parâmetros opcionais do query por cliente e situação](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [Facilitando a alternância do player HLS para fluxos de failover/backup](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [Vários fluxos de taxa de bits](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [Inserção parcial de quebra de anúncio](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [Suporte a vários CDNs para CRS e delivery](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + Substituir linhas do tempo VOD {#replace-vod}
      + [Alterações no VOD](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [Formato de linha do tempo VOD](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [Substituir uma linha do tempo VOD](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + Rastreamento de eficácia do anúncio {#ad}
      + [Rastreamento de anúncios](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [Ativar o rastreamento de anúncios do cliente](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [Visão geral do rastreamento de cliente não TVSDK](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [API para que os players interajam com o servidor manifest](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [Diretiva &quot;EXT-X-MARKER&quot;](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [Cookies](msapi-topics/ms-cookies.md)
   + [Suporte para legendas WebVTT](msapi-topics/ms-webvtt-captions.md)
   + Lista dos formatos de arquivo {#list}
      + [Formatos de arquivo](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [Formato JSON para URL para solicitação de lista de reprodução de manifesto variante](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [Formatos JSON para rastrear URLs](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [Formato VMAP para URLs de rastreamento](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [Requisitos do player de vídeo](msapi-topics/ms-player-req.md)
+ Serviço de reempacotamento da Creative Cloud Primetime {#crs}
   + [Visão geral do SIR](creative-repackaging-service/crs-overview.md)
   + [Principais utilizações do SIR](creative-repackaging-service/jit-async-hls-conv.md)
   + [Suporte a vários CDN](creative-repackaging-service/multi-cdn-supportt.md)
   + [Workflows detalhados para reempacotamento JIT](creative-repackaging-service/jit-repackage.md)
   + [Uso do CRS para injetar tags de metadados cronometradas ID3](creative-repackaging-service/inject-id3.md)
   + [API de reempacotamento](creative-repackaging-service/api-repackage.md)
