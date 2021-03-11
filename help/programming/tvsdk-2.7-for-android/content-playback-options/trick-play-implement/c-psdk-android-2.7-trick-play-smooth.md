---
description: Se o seu sistema tiver acesso à decodificação assistida por hardware, você poderá obter uma reprodução de truques mais suave do que com a implementação TVSDK do software simples usando o formato iFrame.
title: Operações mais suaves de reprodução de truques
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Operações de reprodução de truque mais suaves {#smoother-trick-play-operations}

Se o seu sistema tiver acesso à decodificação assistida por hardware, você poderá obter uma reprodução de truques mais suave do que com a implementação TVSDK do software simples usando o formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

O uso do formato iFrame resulta em operações de reprodução de truques que não são suaves. A operação de reprodução de truques mais suave usa um perfil normal (não iFrame), suporte à decodificação de hardware e uma taxa de quadros aumentada. Diferentes dispositivos de decodificação assistidos por hardware têm diferentes recursos. A velocidade dupla requer 60 quadros por segundo (FPS) e a velocidade quádrupla requer 120 FPS.

>[!IMPORTANT]
>
>O Adobe recomenda que você limite a reprodução para velocidade dupla em dispositivos Android mais recentes e não use o recurso em dispositivos Android mais antigos.

Para obter uma reprodução de truque mais suave, defina `ABRControlParameters.maxPlayoutRate` para o múltiplo desejado da velocidade normal (por exemplo, 2,0 para velocidade dupla). Se uma chamada subsequente para `MediaPlayer.setRate()` tiver um argumento menor ou igual ao valor definido para `maxPlayoutRate`, o TVSDK usará um perfil normal para obter uma reprodução de truque mais suave. Caso contrário, ele usará um perfil de iFrame para a operação de reprodução de trickplay.
