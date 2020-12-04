---
seo-title: Implantar os arquivos WAR
title: Implantar os arquivos WAR
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Implantar os arquivos WAR{#deploy-the-war-files}

1. Copie o arquivo WAR para o diretório [!DNL webapps] de Tomcat.

   * Servidor de individualização: [!DNL flashaccess.war]
   * Servidor de geração de chave: [!DNL flashaccess-kgs.war]

1. Copie a pasta [!DNL ROOT] do pacote fornecido pelo Adobe para o diretório [!DNL webapps].

   O servidor de individualização também precisa hospedar o arquivo [!DNL crossdomain.xml]. (A pasta [!DNL ROOT] contém o arquivo [!DNL crossdomain.xml]; [!DNL ROOT] deve estar em todas as maiúsculas.) O servidor de geração de chave não requer este arquivo.

