---
description: Você pode usar sobreposições HTML com StageVideo para exibir elementos da interface do usuário no plano de vídeo da lista de exibição do Flash. Esse plano está acima do plano StageVideo, de modo que StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição de Flash.
title: Sobreposições de StageVideo e HTML
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Sobreposições de StageVideo e HTML{#stagevideo-and-html-overlays}

Você pode usar sobreposições HTML com StageVideo para exibir elementos da interface do usuário no plano de vídeo da lista de exibição do Flash. Esse plano está acima do plano StageVideo, de modo que StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição de Flash.

As sobreposições HTML são elementos da interface do usuário que podem ser exibidos no plano de exibição do Flash no vídeo renderizado por `StageVideo` em seu próprio plano. Antes do Flash 15, não era possível usar as sobreposições HTML quando a aceleração de hardware não estava disponível. A partir do Flash 15, as sobreposições HTML são exibidas quando `StageVideo` retorna à renderização do software.

>[!IMPORTANT]
>
>Dependendo dos recursos de seu sistema, o desempenho pode degradar-se em maior ou menor grau quando você usa sobreposições HTML.

Considere as seguintes informações:

* No Flash Player 15:

   * Você pode usar sobreposições HTML se a aceleração de hardware estiver disponível.
   * Para usar as sobreposições HTML, defina `wmode` como `opaque`.

* No Flash Player 14:

   * Quando a aceleração de hardware estiver disponível, `StageVideo` fica abaixo da lista de exibição do Flash, para que você possa usar as sobreposições de HTML.
   * Quando a aceleração de hardware não está disponível, o vídeo é renderizado sobre todos os outros elementos no navegador, o que impede o uso de sobreposições HTML.

Estes são os requisitos mínimos do navegador para usar as sobreposições HTML com `StageVideo`:

* Firefox versão 4 e posterior
* Safari versão 4 e posterior
* Internet Explorer:

   * Versão 9+ no Windows 7 e posterior
   * Versão 10+ no Windows XP

* Chrome versão 26 e posterior

   >[!IMPORTANT]
   >
   >Chrome Pepper no Windows XP e Windows Vista não é compatível.

