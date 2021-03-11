---
description: Quando um segmento está ausente, por exemplo, quando um segmento específico falha no download, ele tenta se recuperar por meio de várias tentativas de failover. Se não for possível recuperar, ocorrerá um erro.
title: Failover de segmento ausente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Failover de segmento ausente{#missing-segment-failover}

Quando um segmento está ausente, por exemplo, quando um segmento específico falha no download, ele tenta se recuperar por meio de várias tentativas de failover. Se não for possível recuperar, ocorrerá um erro.

Se um segmento estiver ausente no servidor porque, por exemplo, o arquivo de manifesto não está presente, o segmento não pode ser baixado e, assim por diante, o TVSDK tenta fazer failover tentando as seguintes opções:

1. Tente um failover para o mesmo segmento, na mesma taxa de bits, em um arquivo de variante.
1. Alterne para uma taxa de bits alternativa (switch ABR) no mesmo arquivo.
1. Percorra todas as taxas de bits disponíveis em cada variante disponível.
1. Ignore o segmento e emita um aviso.

Quando o TVSDK não pode obter um segmento alternativo, ele aciona uma notificação de erro `CONTENT_ERROR`. Esta notificação contém uma notificação interna com o código `DOWNLOAD_ERROR`. Se o fluxo com o problema for uma faixa de áudio alternativa, o gera a notificação de erro `AUDIO_TRACK_ERROR`.

Se o mecanismo de vídeo não conseguir obter segmentos continuamente, ele limita o segmento contínuo para 5, depois que a reprodução é interrompida e emite um `NATIVE_ERROR` com o código 5.

>[!NOTE]
>
>Os parâmetros de controle da taxa de bits adaptável (ABR) não são considerados quando ocorre um failover. Isso ocorre porque o mecanismo de failover foi projetado para usar qualquer uma das listas de reprodução atualmente disponíveis, independentemente do perfil de taxa de bits, como fluxos de backup.
>
>Durante uma operação de failover, pode haver um switch de perfil. Se ocorrer um erro durante o download de um dos segmentos da lista de reprodução, os parâmetros de controle ABR, como a taxa de bits mínima/máxima permitida, serão ignorados.

