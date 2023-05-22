---
description: Você pode ativar e criar controles para áudio de associação tardia.
title: Visão geral
exl-id: be3b41c5-1c30-430c-9baa-06b6496aceb4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# Visão geral {#overview}

Você pode ativar e criar controles para áudio de associação tardia.

O padrão HLS permite fluxos multiformato, o que significa que podemos manter os controles de áudio e vídeo de um fluxo separado uns dos outros. A faixa de vídeo, com várias representações (por exemplo, 240p, 480p, 720p e 1080p) e as faixas de áudio (por exemplo, inglês, espanhol, francês, alemão) podem ser codificadas separadamente. O reprodutor de mídia escolhe as faixas de áudio e vídeo desejadas e as vincula em tempo real, no lado do cliente.

Você pode implementar vários workflows, dependendo da interface do usuário do player. O fluxo de trabalho geral para o reprodutor do Primetime é o seguinte:

1. Quando o usuário final seleciona um vídeo, uma lista de faixas de áudio disponíveis para esse item de mídia é preenchida.
1. Quando o usuário toca no botão Configurações na interface do usuário, as opções de trilha de áudio são exibidas.
1. Quando uma faixa de áudio é selecionada, ela se torna a faixa de áudio ativa.
1. O usuário final pode tocar no botão Configurações para voltar para a faixa de áudio original.
