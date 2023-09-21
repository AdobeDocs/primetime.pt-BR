---
description: Quando um segmento está ausente, por exemplo, quando um determinado segmento não é baixado, o tenta se recuperar por meio de várias tentativas de failover. Se não conseguir se recuperar, emitirá um erro.
title: Failover de segmento ausente
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Failover de segmento ausente{#missing-segment-failover}

Quando um segmento está ausente, por exemplo, quando um determinado segmento não é baixado, o tenta se recuperar por meio de várias tentativas de failover. Se não conseguir se recuperar, emitirá um erro.

Se um segmento estiver ausente no servidor porque, por exemplo, o arquivo de manifesto não está presente, o segmento não pode ser baixado e assim por diante, o TVSDK tentará fazer failover tentando as seguintes opções:

1. Tente um failover para o mesmo segmento, na mesma taxa de bits, em um arquivo variante.
1. Alterne para uma taxa de bits alternativa (switch ABR) no mesmo arquivo.
1. Percorra cada taxa de bits disponível em cada variante disponível.
1. Ignore o segmento e emita um aviso.

Quando o TVSDK não pode obter um segmento alternativo, ele aciona um `CONTENT_ERROR` notificação de erro. Esta notificação contém uma notificação interna com o código `DOWNLOAD_ERROR` código. Se o fluxo com o problema for uma faixa de áudio alternativa, o gera a variável `AUDIO_TRACK_ERROR` notificação de erro.

Se o mecanismo de vídeo não conseguir obter segmentos continuamente, ele limita os pulos de segmento contínuo a 5, após os quais a reprodução é interrompida e emite um `NATIVE_ERROR` com o código 5.

>[!NOTE]
>
>Os parâmetros de controle da taxa de bits adaptável (ABR) não são considerados quando ocorre um failover. Isso ocorre porque o mecanismo de failover foi projetado para usar qualquer uma das listas de reprodução disponíveis no momento, independentemente do perfil de taxa de bits, como fluxos de backup.
>
>Durante uma operação de failover, pode haver uma troca de perfil. Se ocorrer um erro durante o download de um dos segmentos da lista de reprodução, os parâmetros de controle ABR, como a taxa de bits mínima/máxima permitida, são ignorados.
