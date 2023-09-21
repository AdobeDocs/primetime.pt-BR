---
description: O TVSDK baixa os segmentos de anúncios e os renderiza na tela do dispositivo.
title: Fase de reprodução do anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Fase de reprodução do anúncio{#ad-playback-phase}

O TVSDK baixa os segmentos de anúncios e os renderiza na tela do dispositivo.

Nesse ponto, o TVSDK resolveu anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As principais classes de erros a seguir podem ocorrer nesta fase:

* Erros ao conectar-se ao servidor host
* Erros ao baixar o arquivo de manifesto
* Erros ao baixar os segmentos de mídia

Para todas as três classes de erro, o TVSDK encaminha eventos acionados para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Os eventos de notificação são acionados quando todas as opções de failover são consideradas e nenhuma ação adicional pode ser executada automaticamente.

  Seu aplicativo precisa tomar a ação apropriada.

Caso ocorram erros, o TVSDK chama onAdBreakComplete para cada `onAdBreakStart` e `onAdComplete` para cada `onAdStart`. No entanto, se não for possível baixar os segmentos, poderá haver lacunas na linha do tempo. Quando as lacunas são grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
