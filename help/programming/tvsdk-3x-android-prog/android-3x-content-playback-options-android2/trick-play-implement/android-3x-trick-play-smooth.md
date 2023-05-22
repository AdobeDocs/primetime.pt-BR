---
description: Se o seu sistema tiver acesso a decodificação assistida por hardware, você poderá obter um truque mais suave do que com a implementação pura do TVSDK por software, usando o formato iFrame.
title: Operações de truque mais suaves
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Operações de truque mais suaves {#smoother-trick-play-operations}

Se o seu sistema tiver acesso a decodificação assistida por hardware, você poderá obter um truque mais suave do que com a implementação pura do TVSDK por software, usando o formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

O uso do formato iFrame resulta em operações de truque de reprodução que não são suaves. A operação de jogo de truque mais suave usa um perfil normal (não iFrame), suporte de decodificação de hardware e uma taxa de quadros aumentada. Diferentes dispositivos de decodificação assistida por hardware têm diferentes recursos. A velocidade dupla requer 60 quadros por segundo (FPS) e a velocidade quádrupla requer 120 FPS.

>[!IMPORTANT]
>
>A Adobe recomenda que você limite a reprodução para uma velocidade dupla em dispositivos Android mais recentes e não use o recurso em dispositivos Android mais antigos.

Para obter um jogo ininterrupto, defina `ABRControlParameters.maxPlayoutRate` para o múltiplo desejado de velocidade normal (por exemplo, 2,0 para velocidade dupla). Se uma chamada subsequente para `MediaPlayer.setRate()` tem um argumento que é menor que ou igual ao valor definido para `maxPlayoutRate`, o TVSDK usa um perfil normal para obter uma reprodução ininterrupta. Caso contrário, ele usa um perfil iFrame para a operação de reprodução.
