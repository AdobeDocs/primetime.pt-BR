---
seo-title: Solução de problemas
title: Solução de problemas
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# Solução de problemas{#troubleshooting}

* Para alguns dispositivos mais antigos que estão executando a API nível 10 ou superior, o logcat não consegue abrir o dispositivo de log devido a um problema de permissões. A seguinte exceção é exibida: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Solução:**

   1. Abra [!DNL AndroidManifest.xml] no projeto [!DNL CatalogActivity] no espaço de trabalho.

   1. Adicione a seguinte permissão ao arquivo [!DNL `AndroidManfest.xml`]:

      ```
      android.permission.READ_LOGS
      ```
