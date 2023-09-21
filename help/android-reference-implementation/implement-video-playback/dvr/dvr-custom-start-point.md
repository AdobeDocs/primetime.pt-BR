---
description: Você pode escolher um ponto de partida personalizado para quando inserir um fluxo DVR, em vez do comportamento padrão de inserir o fluxo DVR no início usando a classe ConfigProvider.
title: Escolhendo um ponto de partida personalizado para DVR
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
