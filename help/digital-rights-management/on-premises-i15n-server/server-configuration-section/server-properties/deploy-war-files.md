---
title: Implantar os arquivos WAR
description: Implantar os arquivos WAR
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# Implantar os arquivos WAR{#deploy-the-war-files}

1. Copie o arquivo WAR para o do Tomcat [!DNL webapps] diretório.

   * Servidor de individualização: [!DNL flashaccess.war]
   * Servidor de Geração de Chave: [!DNL flashaccess-kgs.war]

1. Copie o [!DNL ROOT] pasta do pacote fornecido pelo Adobe para o [!DNL webapps] diretório.

   O servidor de individualização também precisa hospedar o [!DNL crossdomain.xml] arquivo. (O [!DNL ROOT] a pasta contém o [!DNL crossdomain.xml] arquivo; [!DNL ROOT] deve estar em maiúsculas.) O servidor de Geração de Chaves não requer esse arquivo.
