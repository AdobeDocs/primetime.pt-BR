---
description: Os eventos do TVSDK indicam o status do player, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
seo-description: Os eventos do TVSDK indicam o status do player, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
seo-title: Analisar eventos do Primetime Player
title: Analisar eventos do Primetime Player
uuid: bd0a428c-fa51-41a6-950a-9d6843c6e177
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Visão geral {#listen-for-primetime-player-events-overview}

Os eventos do TVSDK indicam o status do player, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.

Como seu aplicativo precisa responder a muitos desses eventos, é necessário implementar rotinas de manipulação de eventos e registrar essas rotinas no TVSDK. As rotinas chamam os métodos TVSDK relevantes para responder adequadamente.

Mais informações sobre eventos:

* A natureza em tempo real da reprodução de vídeo requer atividade assíncrona (não bloqueada) para muitas operações TVSDK.
* O TVSDK suporta um player de vídeo controlado por evento.

   Fornece eventos que correspondem a todas as etapas importantes do processo de reprodução. Você registra esses eventos no mecanismo de eventos da sua plataforma e cria manipuladores de eventos que serão chamados quando esses eventos ocorrerem. *`Event Handlers`* também são conhecidos como rotinas de retorno de chamada ou ouvintes de evento. O TVSDK fornece uma gama completa de métodos que podem ser usados pelos manipuladores de eventos.
* O aplicativo geralmente inicia operações não bloqueadas, como solicitar que um vídeo comece a ser reproduzido.

   O TVSDK se comunica de forma assíncrona com seu aplicativo enviando eventos, como quando o vídeo começa a ser reproduzido e um evento quando o vídeo termina. Outros eventos podem indicar alterações de status no player e condições de erro. Seus manipuladores de eventos tomam as ações apropriadas.