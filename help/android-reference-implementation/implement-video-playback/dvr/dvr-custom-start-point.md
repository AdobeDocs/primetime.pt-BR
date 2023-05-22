---
description: Você pode escolher um ponto de partida personalizado para quando inserir um fluxo DVR, em vez do comportamento padrão de inserir o fluxo DVR no início usando a classe ConfigProvider.
title: Escolhendo um ponto de partida personalizado para DVR
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Escolhendo um ponto de partida personalizado para DVR {#choosing-a-custom-starting-point-for-dvr}

Você pode escolher um ponto de partida personalizado para quando inserir um fluxo DVR, em vez do comportamento padrão de inserir o fluxo DVR no início usando a classe ConfigProvider.

Para definir a hora de início até a variável [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) classe:

1. Ativar [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Definir a hora de início em [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Verifique se a posição inicial personalizada está habilitada.
