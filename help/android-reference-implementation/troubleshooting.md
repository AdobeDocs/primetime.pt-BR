---
title: Solução de problemas
description: Solução de problemas
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
