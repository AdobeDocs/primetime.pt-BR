---
description: Se o seu sistema tiver acesso à decodificação assistida por hardware, você poderá obter uma reprodução de truques mais suave do que com a implementação pura de TVSDK de software usando o formato iFrame.
seo-description: Se o seu sistema tiver acesso à decodificação assistida por hardware, você poderá obter uma reprodução de truques mais suave do que com a implementação pura de TVSDK de software usando o formato iFrame.
seo-title: Operações de play de truque mais suaves
title: Operações de play de truque mais suaves
uuid: 4749bfa0-17bf-4444-a167-987249945325
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Operações de play de truque mais suaves {#smoother-trick-play-operations}

Se o seu sistema tiver acesso à decodificação assistida por hardware, você poderá obter uma reprodução de truques mais suave do que com a implementação pura de TVSDK de software usando o formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

O uso do formato iFrame resulta em operações de reprodução de truques que não são suaves. A operação de reprodução de truques mais suave usa um perfil normal (não iFrame), suporte à decodificação de hardware e uma taxa de quadros aumentada. Diferentes dispositivos de decodificação assistidos por hardware têm diferentes capacidades. A velocidade dupla requer 60 quadros por segundo (FPS) e a velocidade quádrupla requer 120 FPS.

>[!IMPORTANT]
>
>A Adobe recomenda que você limite a reprodução para velocidade dupla para dispositivos Android mais recentes e não use o recurso para dispositivos Android mais antigos.

Para obter uma reprodução de truque mais suave, defina `ABRControlParameters.maxPlayoutRate` para o múltiplo desejado de velocidade normal (por exemplo, 2.0 para velocidade dupla). Se uma chamada subsequente para `MediaPlayer.setRate()` tiver um argumento menor ou igual ao valor definido para `maxPlayoutRate`, o TVSDK usará um perfil normal para obter uma reprodução de truque mais suave. Caso contrário, ele usa um perfil do iFrame para a operação de trickplay.
