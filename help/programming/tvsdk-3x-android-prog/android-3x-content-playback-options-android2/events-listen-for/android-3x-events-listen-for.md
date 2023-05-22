---
description: Os eventos do TVSDK indicam o status do reprodutor, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
title: Analise eventos do Primetime Player
exl-id: 3d626890-0384-46b0-b4b7-cfc462e1da07
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Visão geral {#listen-for-primetime-player-events-overview}

Os eventos do TVSDK indicam o status do reprodutor, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.

Como seu aplicativo precisa responder a muitos desses eventos, é necessário implementar rotinas de manipulação de eventos e registrá-las com o TVSDK. As rotinas chamam os métodos TVSDK relevantes para responder adequadamente.

Mais informações sobre eventos:

* A natureza em tempo real da reprodução de vídeo requer atividade assíncrona (não de bloqueio) para muitas operações de TVSDK.
* O TVSDK é compatível com um reprodutor de vídeo orientado por eventos.

   Ele fornece eventos que correspondem a todas as etapas importantes do processo de reprodução. Registre esses eventos no mecanismo de eventos da sua plataforma e crie manipuladores de eventos que serão chamados quando esses eventos ocorrerem. *`Event Handlers`* também são conhecidas como rotinas de retorno de chamada ou ouvintes de eventos. O TVSDK fornece uma variedade completa de métodos que podem ser usados pelos manipuladores de eventos.
* Seu aplicativo geralmente inicia operações não bloqueadas, como solicitar que um vídeo comece a ser reproduzido.

   O TVSDK se comunica de forma assíncrona com seu aplicativo despachando eventos, como quando o vídeo começa a ser reproduzido e um evento quando o vídeo é concluído. Outros eventos podem indicar alterações de status no reprodutor e condições de erro. Seus manipuladores de eventos executam as ações apropriadas.
