---
title: Implantar a implementação de referência BEES
description: Implantar a implementação de referência BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# Implantar a implementação de referência do BEES {#deploy-the-bees-reference-implementation}

1. Configure seu servidor de aplicativos Tomcat. (Consulte a documentação do Tomcat.)
1. Copie o arquivo `[!DNL bees.war]` na pasta [!DNL webapps/] do Tomcat.
1. Envie uma solicitação para `https://localhost:8080/bees`.

   Se você vir uma mensagem &quot;O BEES é operacional&quot;, a implantação é concluída com êxito.
1. Ative o SSL no servidor.
