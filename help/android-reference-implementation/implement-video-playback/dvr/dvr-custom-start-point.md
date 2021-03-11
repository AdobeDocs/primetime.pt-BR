---
description: Você pode escolher um ponto de partida personalizado para quando inserir um fluxo de DVR em vez do comportamento padrão de inserir o fluxo de DVR no início usando a classe ConfigProvider.
title: Escolha de um ponto de partida personalizado para DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Escolha de um ponto de partida personalizado para DVR {#choosing-a-custom-starting-point-for-dvr}

Você pode escolher um ponto de partida personalizado para quando inserir um fluxo de DVR em vez do comportamento padrão de inserir o fluxo de DVR no início usando a classe ConfigProvider.

Para definir a hora de início por meio da classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html):

1. Habilite [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Defina a hora de início em [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Verifique se a posição inicial personalizada está ativada.
