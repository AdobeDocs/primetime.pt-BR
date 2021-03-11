---
title: Solução de problemas
description: Solução de problemas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# Solução de problemas{#troubleshooting}

* Para alguns dispositivos mais antigos que estão executando o nível 10 ou mais da API, o logcat não pode abrir o dispositivo de log devido a um problema de permissões. A seguinte exceção é exibida: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Solução alternativa:**

   1. Abra [!DNL AndroidManifest.xml] no projeto [!DNL CatalogActivity] no espaço de trabalho.

   1. Adicione a seguinte permissão ao arquivo [!DNL `AndroidManfest.xml`]:

      ```
      android.permission.READ_LOGS
      ```
