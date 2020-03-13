---
description: Quando a reprodução atinge uma pausa de anúncio, passa uma pausa de anúncio ou termina em uma pausa de anúncio, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
seo-description: Quando a reprodução atinge uma pausa de anúncio, passa uma pausa de anúncio ou termina em uma pausa de anúncio, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
seo-title: Personalizar reprodução com anúncios
title: Personalizar reprodução com anúncios
uuid: e0d3dfb2-b2d2-4590-aa19-26bea916a252
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visão geral {#customize-playback-with-ads}

Quando a reprodução atinge uma pausa de anúncio, passa uma pausa de anúncio ou termina em uma pausa de anúncio, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.

>[!TIP]
>
>Você pode substituir o comportamento padrão usando a `AdBreakPolicySelector` classe.

O comportamento padrão varia, dependendo se o usuário passa no intervalo do anúncio durante a reprodução normal ou procurando em um vídeo ou reposicionando-o com avanço rápido ou retrocesso (peça).

Você pode personalizar o comportamento de reprodução de anúncios das seguintes maneiras:

* Salve a posição na qual o usuário parou de assistir ao vídeo e retomará a reprodução na mesma posição em uma sessão futura.
* Se uma pausa de anúncio for apresentada ao usuário, não exiba anúncios adicionais por alguns minutos, mesmo se o usuário buscar uma nova posição.
* Se o conteúdo não for reproduzido após alguns minutos, reinicie o fluxo ou faça failover para uma fonte diferente para o mesmo conteúdo.

Na sessão de reprodução de failover, para permitir que o usuário pule os anúncios e retome para a posição anterior com falha, você pode desativar os anúncios anteriores e/ou intermediários. O TVSDK fornece métodos para permitir a omissão de anúncios precedentes e intermediários.