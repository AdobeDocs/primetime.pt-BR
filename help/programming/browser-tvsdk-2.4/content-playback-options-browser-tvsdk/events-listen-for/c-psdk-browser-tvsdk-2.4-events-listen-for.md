---
description: Os eventos do TVSDK do navegador indicam o estado do reprodutor, os erros que ocorrem, a conclusão de ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
title: Analise os eventos do Player do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Visão geral {#listen-for-primetime-player-events-overview}

Os eventos do TVSDK do navegador indicam o estado do reprodutor, os erros que ocorrem, a conclusão de ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.

Como seu aplicativo precisa responder a muitos desses eventos, é necessário implementar rotinas de apresentação de eventos e registrar essas rotinas com TVSDK do navegador. As rotinas chamam os métodos TVSDK do navegador relevantes para responder adequadamente.

Estas são algumas informações adicionais sobre eventos:

* A natureza em tempo real da reprodução de vídeo requer uma atividade assíncrona (não bloqueada) para muitas operações de TVSDK do navegador.
* O TVSDK do navegador é compatível com um reprodutor de vídeo controlado por evento.

   Ele fornece eventos que correspondem a todas as etapas importantes no processo de reprodução. Você registra esses eventos no mecanismo de evento da plataforma e cria manipuladores de eventos que serão chamados quando esses eventos ocorrerem. *`Event Handlers`* também são conhecidos como rotinas de retorno de chamada ou ouvintes de eventos. O TVSDK do navegador fornece um intervalo completo de métodos que podem ser usados pelos manipuladores de evento.
* O aplicativo geralmente inicia operações que não são de bloqueio, como solicitar que um vídeo comece a ser reproduzido.

   O TVSDK do navegador se comunica de forma assíncrona com seu aplicativo ao despachar eventos, como quando o vídeo começa a ser reproduzido e um evento quando o vídeo termina. Outros eventos podem indicar alterações de status no reprodutor e condições de erro. Seus manipuladores de evento tomam as ações apropriadas.

