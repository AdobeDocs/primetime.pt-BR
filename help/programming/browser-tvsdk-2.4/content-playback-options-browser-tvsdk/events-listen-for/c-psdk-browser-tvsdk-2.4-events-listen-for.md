---
description: Os eventos do TVSDK do navegador indicam o estado do reprodutor, erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou ações que ocorrem implicitamente, como a conclusão de um anúncio.
title: Analise eventos do Primetime Player
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Visão geral {#listen-for-primetime-player-events-overview}

Os eventos do TVSDK do navegador indicam o estado do reprodutor, erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou ações que ocorrem implicitamente, como a conclusão de um anúncio.

Como seu aplicativo precisa responder a muitos desses eventos, é necessário implementar rotinas de entrega de eventos e registrar essas rotinas com o TVSDK do navegador. As rotinas chamam os métodos TVSDK do navegador relevantes para responder adequadamente.

Estas são algumas informações adicionais sobre eventos:

* A natureza em tempo real da reprodução de vídeo requer atividade assíncrona (não de bloqueio) para muitas operações de TVSDK do navegador.
* O TVSDK do navegador é compatível com um reprodutor de vídeo orientado por eventos.

  Ele fornece eventos que correspondem a todas as etapas importantes do processo de reprodução. Registre esses eventos no mecanismo de eventos da sua plataforma e crie manipuladores de eventos que serão chamados quando esses eventos ocorrerem. *`Event Handlers`* também são conhecidas como rotinas de retorno de chamada ou ouvintes de eventos. O TVSDK do navegador fornece uma variedade completa de métodos que podem ser usados pelos manipuladores de eventos.
* Seu aplicativo geralmente inicia operações não bloqueadas, como solicitar que um vídeo comece a ser reproduzido.

  O TVSDK do navegador se comunica de forma assíncrona com seu aplicativo despachando eventos, como quando o vídeo começa a ser reproduzido e um evento quando o vídeo é concluído. Outros eventos podem indicar alterações de status no reprodutor e condições de erro. Seus manipuladores de eventos executam as ações apropriadas.
