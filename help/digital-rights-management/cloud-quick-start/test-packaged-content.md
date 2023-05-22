---
title: Testar o conteúdo do pacote
description: Testar o conteúdo do pacote
copied-description: true
exl-id: 98456bf8-5d4d-47a7-905a-e6dac1e826ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Testar o conteúdo do pacote {#test-the-packaged-content}

Você deve validar se a operação de empacotamento foi bem-sucedida usando o Adobe Primetime Desktop Player disponível publicamente (por meio do Flash Player). Este player só oferece suporte a conteúdo HDS. Para testar o conteúdo HLS, é necessário um player habilitado para TVSDK do Navegador do Primetime.

1. Hospede seu conteúdo em um servidor da Web.
1. Inicie o reprodutor Primetime DRM (anteriormente chamado de Acesso ao Adobe) em https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Cole o URL no manifesto HDS ( [!DNL .f4m]) no campo de navegação do reprodutor e clique no botão **[!UICONTROL Play]** botão.
