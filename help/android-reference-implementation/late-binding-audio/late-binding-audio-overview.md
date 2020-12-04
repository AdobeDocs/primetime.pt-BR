---
description: Você pode ativar e criar controles para áudio de ligação tardia.
seo-description: Você pode ativar e criar controles para áudio de ligação tardia.
seo-title: Visão geral
title: Visão geral
uuid: 7656f930-f426-426e-bcd4-dfa9d39e7ae4
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Visão geral {#overview}

Você pode ativar e criar controles para áudio de ligação tardia.

O padrão HLS permite fluxos de vários formatos, o que significa que podemos manter as faixas de áudio e vídeo de um fluxo separadas umas das outras. A faixa de vídeo, com várias execuções (por exemplo, 240p, 480p, 720p e 1080p) e as faixas de áudio (por exemplo, inglês, espanhol, francês, alemão) podem ser codificadas separadamente. O player de mídia escolhe as faixas de vídeo e áudio desejadas e as vincula dinamicamente, no lado do cliente.

Você pode implementar vários workflows, dependendo da interface do usuário do player. O fluxo de trabalho geral do player do Primetime é o seguinte:

1. Quando o usuário final seleciona um vídeo, uma lista de faixas de áudio disponíveis para esse item de mídia é preenchida.
1. Quando o usuário toca no botão Configurações na interface do usuário, as opções da faixa de áudio são exibidas.
1. Quando uma faixa de áudio é selecionada, a faixa se torna a faixa de áudio ativa.
1. O usuário final pode tocar no botão Configurações para alternar de volta para a faixa de áudio original.

