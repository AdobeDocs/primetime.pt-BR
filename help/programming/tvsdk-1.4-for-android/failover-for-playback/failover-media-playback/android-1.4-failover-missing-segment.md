---
description: Quando um segmento está ausente, por exemplo, quando um segmento específico falha no download, tenta se recuperar por meio de várias tentativas de failover. Se não conseguir recuperar, isso emite um erro.
seo-description: Quando um segmento está ausente, por exemplo, quando um segmento específico falha no download, tenta se recuperar por meio de várias tentativas de failover. Se não conseguir recuperar, isso emite um erro.
seo-title: Failover de segmento ausente
title: Failover de segmento ausente
uuid: 17ee1221-e1eb-4f64-a406-4d7eff1d7555
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Failover de segmento ausente{#missing-segment-failover}

Quando um segmento está ausente, por exemplo, quando um segmento específico falha no download, tenta se recuperar por meio de várias tentativas de failover. Se não conseguir recuperar, isso emite um erro.

Se um segmento estiver ausente no servidor porque, por exemplo, o arquivo manifest não está presente, o segmento não pode ser baixado e assim por diante, o TVSDK tenta fazer failover tentando as seguintes opções:

1. Tente um failover para o mesmo segmento, na mesma taxa de bits, em um arquivo de variante.
1. Alterne para uma taxa de bits alternativa (switch ABR) no mesmo arquivo.
1. Faça o ciclo de cada taxa de bits disponível em cada variante disponível.
1. Ignore o segmento e emita um aviso.

Quando o TVSDK não pode obter um segmento alternativo, ele aciona uma notificação de `CONTENT_ERROR` erro. Esta notificação contém uma notificação interna com o código `DOWNLOAD_ERROR` . Se o fluxo com o problema for uma faixa de áudio alternativa, gerará a notificação de `AUDIO_TRACK_ERROR` erro.

Se o mecanismo de vídeo não conseguir obter segmentos continuamente, ele limita o segmento contínuo a saltar para 5, após o qual a reprodução é interrompida e emite um `NATIVE_ERROR` erro com o código 5.

>[!NOTE]
>
>Os parâmetros de controle da taxa de bits adaptável (ABR) não são considerados quando ocorre um failover. Isso ocorre porque o mecanismo de failover foi projetado para usar qualquer uma das listas de reprodução disponíveis no momento, independentemente do perfil de taxa de bits, como fluxos de backup.
>
>Durante uma operação de failover, pode haver um switch de perfil. Se ocorrer um erro durante o download de um dos segmentos da lista de reprodução, os parâmetros de controle ABR, como a taxa de bits mínima/máxima permitida, serão ignorados.

