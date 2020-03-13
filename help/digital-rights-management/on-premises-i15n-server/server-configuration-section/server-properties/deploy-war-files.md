---
seo-title: Implantar os arquivos WAR
title: Implantar os arquivos WAR
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Implantar os arquivos WAR{#deploy-the-war-files}

1. Copie o arquivo WAR para o [!DNL webapps] diretório de Tomcat.

   * Servidor de individualização: [!DNL flashaccess.war]
   * Servidor de geração de chave: [!DNL flashaccess-kgs.war]

1. Copie a [!DNL ROOT] pasta do pacote fornecido pela Adobe para o [!DNL webapps] diretório.

   O servidor de individualização também precisa hospedar o [!DNL crossdomain.xml] arquivo. (A [!DNL ROOT] pasta contém o [!DNL crossdomain.xml] arquivo; deve [!DNL ROOT] estar em todos os limites.) O servidor de geração de chave não requer este arquivo.

