---
title: Implantar os arquivos WAR
description: Implantar os arquivos WAR
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Implantar os arquivos WAR{#deploy-the-war-files}

1. Copie o arquivo WAR para o diretório [!DNL webapps] do Tomcat.

   * Servidor de individualização: [!DNL flashaccess.war]
   * Servidor de geração de chave: [!DNL flashaccess-kgs.war]

1. Copie a pasta [!DNL ROOT] do pacote fornecido pelo Adobe para o diretório [!DNL webapps].

   O servidor de individualização também precisa hospedar o arquivo [!DNL crossdomain.xml] . (A pasta [!DNL ROOT] contém o arquivo [!DNL crossdomain.xml]; [!DNL ROOT] deve estar em todas as maiúsculas.) O servidor de Geração de Chave não requer este arquivo.

