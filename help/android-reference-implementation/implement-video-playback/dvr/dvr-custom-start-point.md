---
description: Você pode escolher um ponto de partida personalizado para quando inserir um fluxo DVR em vez do comportamento padrão de inserir o fluxo DVR no início usando a classe ConfigProvider.
seo-description: Você pode escolher um ponto de partida personalizado para quando inserir um fluxo DVR em vez do comportamento padrão de inserir o fluxo DVR no início usando a classe ConfigProvider.
seo-title: Escolhendo um ponto de partida personalizado para DVR
title: Escolhendo um ponto de partida personalizado para DVR
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Escolhendo um ponto de partida personalizado para DVR {#choosing-a-custom-starting-point-for-dvr}

Você pode escolher um ponto de partida personalizado para quando inserir um fluxo DVR em vez do comportamento padrão de inserir o fluxo DVR no início usando a classe ConfigProvider.

Para definir a hora de início pela classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) :

1. Habilitar [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Defina a hora de início em [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Verifique se a posição inicial personalizada está ativada.
