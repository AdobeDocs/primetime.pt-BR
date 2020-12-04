---
description: Eventos do TVSDK do navegador indicam o estado do player, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
seo-description: Eventos do TVSDK do navegador indicam o estado do player, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
seo-title: Ouça eventos do Primetime Player
title: Ouça eventos do Primetime Player
uuid: 7b7c28ac-22ae-46a3-bbeb-bef1b04baeb3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Visão geral {#listen-for-primetime-player-events-overview}

Eventos do TVSDK do navegador indicam o estado do player, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.

Como seu aplicativo precisa responder a muitos desses eventos, é necessário implementar rotinas de manipulação de eventos e registrar essas rotinas com o TVSDK do navegador. As rotinas chamam os métodos TVSDK do navegador relevantes para responder adequadamente.

Estas são algumas informações adicionais sobre eventos:

* A natureza em tempo real da reprodução de vídeo requer atividade assíncrona (não bloqueada) para muitas operações TVSDK do navegador.
* O TVSDK do navegador suporta um player de vídeo controlado por evento.

   Fornece eventos que correspondem a todas as etapas importantes do processo de reprodução. Você registra esses eventos no mecanismo de evento da sua plataforma e cria manipuladores de eventos que serão chamados quando esses eventos ocorrerem. *`Event Handlers`* também são conhecidos como rotinas de retorno de chamada ou ouvintes de evento. O TVSDK do navegador fornece uma gama completa de métodos que podem ser usados pelos manipuladores de eventos.
* O aplicativo geralmente inicia operações não bloqueadas, como solicitar a reprodução de um start de vídeo.

   O TVSDK do navegador se comunica de forma assíncrona com seu aplicativo enviando eventos, como quando os start de vídeo são reproduzidos e um evento quando o vídeo é concluído. Outros eventos podem indicar mudanças de status no player e condições de erro. Seus manipuladores de evento executam as ações apropriadas.

