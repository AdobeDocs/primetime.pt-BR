---
description: Você pode usar sobreposições HTML com StageVideo para exibir elementos de interface no plano de vídeo da lista de exibição Flash. Esse plano está acima do plano StageVideo, portanto, o StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição Flash.
seo-description: Você pode usar sobreposições HTML com StageVideo para exibir elementos de interface no plano de vídeo da lista de exibição Flash. Esse plano está acima do plano StageVideo, portanto, o StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição Flash.
seo-title: Sobreposições de StageVideo e HTML
title: Sobreposições de StageVideo e HTML
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Sobreposições de StageVideo e HTML{#stagevideo-and-html-overlays}

Você pode usar sobreposições HTML com StageVideo para exibir elementos de interface no plano de vídeo da lista de exibição Flash. Esse plano está acima do plano StageVideo, portanto, o StageVideo sempre é exibido atrás de qualquer elemento da lista de exibição Flash.

As sobreposições HTML são elementos da interface que você pode exibir no plano de exibição Flash no vídeo que é renderizado `StageVideo` em seu próprio plano. Antes do Flash 15, não era possível usar sobreposições HTML quando a aceleração de hardware não estava disponível. A partir do Flash 15, as sobreposições HTML são exibidas quando `StageVideo` retorna à renderização do software.

>[!IMPORTANT]
>
>Dependendo das capacidades do seu sistema, o desempenho pode diminuir para um grau maior ou menor quando você usa sobreposições HTML.

Considere as seguintes informações:

* No Flash Player 15:

   * Você pode usar sobreposições HTML se a aceleração por hardware estiver disponível.
   * Para usar sobreposições HTML, defina `wmode` como `opaque`.

* No Flash Player 14:

   * Quando a aceleração de hardware estiver disponível, `StageVideo` estará abaixo da lista de exibição Flash, para que você possa usar sobreposições HTML.
   * Quando a aceleração de hardware não está disponível, o vídeo é renderizado sobre todos os outros elementos no navegador, o que impede o uso de sobreposições HTML.

Estes são os requisitos mínimos do navegador para usar sobreposições HTML com `StageVideo`:

* Firefox versão 4 e posterior
* Safari versão 4 e posterior
* Internet Explorer:

   * Versão 9+ no Windows 7 e posterior
   * Versão 10+ no Windows XP

* Chrome versão 26 e posterior

   >[!IMPORTANT]
   >
   >Chrome Pepper no Windows XP e Windows Vista não é compatível.

