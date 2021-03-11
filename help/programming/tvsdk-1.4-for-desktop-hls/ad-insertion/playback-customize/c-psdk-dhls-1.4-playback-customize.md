---
description: Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
title: Personalizar reprodução com anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Visão geral {#customize-playback-with-ads-overview}

Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.

>[!TIP]
>
>Você pode substituir o comportamento padrão usando a classe `AdPolicySelector`.

O comportamento padrão varia, dependendo se o usuário passa o ad break durante a reprodução normal ou procurando em um vídeo ou reposicionando-o com avanço rápido ou retrocesso (reprodução de truque).

Você pode personalizar o comportamento da reprodução de anúncio das seguintes maneiras:

* Salve a posição em que o usuário parou de assistir ao vídeo e retomou a reprodução na mesma posição em uma sessão futura.
* Se um ad break for apresentado ao usuário, ele não exibirá anúncios adicionais por alguns minutos, mesmo se o usuário buscar uma nova posição.
* Se o conteúdo não for reproduzido após alguns minutos, reinicie o fluxo ou faça failover para uma fonte diferente para o mesmo conteúdo.

   Na sessão de reprodução de failover, para permitir que o usuário ignore os anúncios e retome para a posição de falha anterior, é possível desativar os anúncios precedentes e/ou intermediários. O TVSDK fornece métodos para permitir a ignorância de anúncios precedentes e intermediários.