---
description: O TVSDK baixa os segmentos do anúncio e os renderiza na tela do dispositivo.
seo-description: O TVSDK baixa os segmentos do anúncio e os renderiza na tela do dispositivo.
seo-title: Fase de reprodução do anúncio
title: Fase de reprodução do anúncio
uuid: 1bbcea08-3475-4a64-9f89-c455d5dd828e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Fase de reprodução do anúncio{#ad-playback-phase}

O TVSDK baixa os segmentos do anúncio e os renderiza na tela do dispositivo.

Nesse ponto, o TVSDK resolveu os anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As seguintes classes principais de erros podem ocorrer nesta fase:

* Erros ao conectar ao servidor host
* Erros ao baixar o arquivo manifest
* Erros ao baixar segmentos de mídia

Para todas as três classes de erro, o TVSDK encaminhou eventos para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Eventos de notificação acionados quando todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Independentemente de ocorrerem erros, o TVSDK chama onAdBreakComplete para cada `onAdBreakStart` e `onAdComplete` para cada `onAdStart`. No entanto, se os segmentos não puderem ser baixados, pode haver lacunas na linha do tempo. Quando as lacunas forem grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
