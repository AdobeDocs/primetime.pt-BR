---
description: Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
title: Personalizar reprodução com anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Visão geral {#customize-playback-with-ads-overview}

Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.

>[!TIP]
>
>Você pode substituir o comportamento padrão usando o `AdBreakPolicySelector` classe.

O comportamento padrão varia, dependendo se o usuário passa o ad break durante a reprodução normal ou se busca em um vídeo ou o reposiciona com avanço rápido ou retrocesso (reprodução de truque).

Você pode personalizar o comportamento de reprodução das seguintes maneiras:

* Salve a posição em que o usuário parou de assistir ao vídeo e retome a reprodução na mesma posição em uma sessão futura.
* Se um ad break for apresentado ao usuário, ele não exibirá anúncios adicionais por alguns minutos, mesmo se o usuário buscar uma nova posição.
* Se o conteúdo não for reproduzido após alguns minutos, reinicie o fluxo ou faça failover para uma origem diferente para o mesmo conteúdo.

  Na sessão de reprodução de failover, para permitir que o usuário ignore os anúncios e retome para a posição de falha anterior, é possível desativar os anúncios precedentes e/ou intermediários. O TVSDK fornece métodos para permitir ignorar anúncios precedentes e intermediários.
