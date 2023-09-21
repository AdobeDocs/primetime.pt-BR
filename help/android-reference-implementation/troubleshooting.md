---
title: Solução de problemas
description: Solução de problemas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Solução de problemas{#troubleshooting}

* Em alguns dispositivos mais antigos que executam a API de nível 10 ou mais antiga, o logcat não consegue abrir o dispositivo de log devido a um problema de permissões. A seguinte exceção é exibida: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Solução alternativa:**

   1. Abertura [!DNL AndroidManifest.xml] no [!DNL CatalogActivity] projeto no espaço de trabalho.

   1. Adicione a seguinte permissão à [!DNL `AndroidManfest.xml`] arquivo:

      ```
      android.permission.READ_LOGS
      ```
