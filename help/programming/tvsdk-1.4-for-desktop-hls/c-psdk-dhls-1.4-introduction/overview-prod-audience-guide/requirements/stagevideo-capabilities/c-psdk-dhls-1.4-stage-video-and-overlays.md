---
description: Você pode usar sobreposições de HTML com StageVideo para exibir elementos da interface no plano de vídeo da lista de exibição do Flash. Esse plano está acima do plano StageVideo, portanto, StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição do Flash.
title: Sobreposições StageVideo e HTML
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Sobreposições StageVideo e HTML{#stagevideo-and-html-overlays}

Você pode usar sobreposições de HTML com StageVideo para exibir elementos da interface no plano de vídeo da lista de exibição do Flash. Esse plano está acima do plano StageVideo, portanto, StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição do Flash.

as sobreposições de HTML são elementos da interface do usuário que podem ser exibidos no plano de exibição do Flash em um vídeo renderizado por `StageVideo` no seu próprio plano. Antes do Flash 15, você não podia usar sobreposições de HTML quando a aceleração de hardware não estava disponível. A partir do Flash 15, as sobreposições de HTML são exibidas quando `StageVideo` retorna à renderização de software.

>[!IMPORTANT]
>
>Dependendo das capacidades do seu sistema, o desempenho pode ser degradado em maior ou menor grau com o uso de sobreposições de HTML.

Considere as seguintes informações:

* No Flash Player 15:

   * Você pode usar as sobreposições de HTML se a aceleração de hardware estiver disponível.
   * Para usar sobreposições de HTML, defina `wmode` para `opaque`.

* No Flash Player 14:

   * Quando a aceleração de hardware estiver disponível, `StageVideo` O fica abaixo da lista de exibição do Flash, para que você possa usar as sobreposições de HTML.
   * Quando a aceleração de hardware não está disponível, o vídeo é renderizado sobre todos os outros elementos no navegador, o que impede o uso de sobreposições de HTML.

Estes são os requisitos mínimos do navegador para usar sobreposições de HTML com `StageVideo`:

* Firefox versão 4 e posterior
* Safari versão 4 e posterior
* Internet Explorer:

   * Versão 9+ no Windows 7 e posterior
   * Versão 10+ no Windows XP

* Chrome versão 26 e posterior

  >[!IMPORTANT]
  >
  >O Chrome Pepper no Windows XP e no Windows Vista não é compatível.
