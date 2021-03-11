---
description: O TVSDK baixa os segmentos de publicidade e os renderiza na tela do dispositivo.
title: Fase de reprodução do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Fase de reprodução de anúncio{#ad-playback-phase}

O TVSDK baixa os segmentos de publicidade e os renderiza na tela do dispositivo.

Nesse momento, o TVSDK resolveu os anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As principais classes de erros a seguir podem ocorrer nesta fase:

* Erros ao conectar ao servidor host
* Erros ao baixar o arquivo manifest
* Erros ao baixar os segmentos de mídia

Para todas as três classes de erro, o TVSDK encaminha eventos acionados para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Eventos de notificação acionados quando todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Se ocorrerem erros ou não, o TVSDK chama onAdBreakComplete para cada `onAdBreakStart` e `onAdComplete` para cada `onAdStart`. No entanto, se os segmentos não puderem ser baixados, pode haver lacunas na linha do tempo. Quando as lacunas são grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
