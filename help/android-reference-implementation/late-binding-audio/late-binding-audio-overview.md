---
description: Você pode ativar e criar controles para o áudio de ligação tardia.
title: Visão geral
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Visão geral {#overview}

Você pode ativar e criar controles para o áudio de ligação tardia.

O padrão HLS permite fluxos de vários formatos, o que significa que podemos manter as faixas de áudio e vídeo de um fluxo separado umas das outras. A faixa de vídeo, com várias representações (por exemplo, 240p, 480p, 720p e 1080p) e as faixas de áudio (por exemplo, inglês, espanhol, francês, alemão) podem ser codificadas separadamente. O reprodutor de mídia escolhe as trilhas de vídeo e áudio desejadas e as vincula em tempo real, no lado do cliente.

Você pode implementar vários fluxos de trabalho, dependendo da interface do usuário do player. O fluxo de trabalho geral do player do Primetime é o seguinte:

1. Quando o usuário final seleciona um vídeo, uma lista de faixas de áudio disponíveis para esse item de mídia é preenchida.
1. Quando o usuário toca no botão Configurações na interface do usuário, as opções de faixa de áudio são exibidas.
1. Quando uma faixa de áudio é selecionada, a faixa se torna a faixa de áudio ativa.
1. O usuário final pode tocar no botão Configurações para voltar para a faixa de áudio original.

