---
title: Otimizar os tempos de inicialização do vídeo
description: Otimização dos tempos de inicialização do vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Otimizar a visão geral dos tempos de inicialização do vídeo {#optimize-video-start-up-times}

O Ad Insertion do Primetime fornece vários recursos para otimizar o tempo de inicialização do vídeo, como armazenamento em cache e regras para otimização de rota/protocolo. Estas são algumas outras recomendações para garantir tempos mais rápidos de inicialização de vídeo ao usar o Ad Insertion do Primetime:

* Veicular todos os anúncios e conteúdo de Redes de entrega de conteúdo (CDNs)

* Reduza ou remova handshakes de TLS entre o Ad Insertion do Primetime e os CDNs. Para obter mais informações, consulte [Otimizar rotas e protocolos](optimize-routes-protocols.md).

* Veicular fragmentos de anúncio e conteúdo da mesma CDN

* Inserir cabeçalhos de controle de cache para conteúdo ativo/VOD e manifestos

* Reduzir ou remover provedores de anúncios ou criadores de anúncios lentos na resposta
