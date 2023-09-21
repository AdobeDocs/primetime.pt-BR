---
title: Implantar a implementação de referência do BEES
description: Implantar a implementação de referência do BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# Implantar a implementação de referência do BEES {#deploy-the-bees-reference-implementation}

1. Configure seu servidor de aplicativos Tomcat. (Consulte a documentação do Tomcat.)
1. Copie o `[!DNL bees.war]` arquivo no do Tomcat [!DNL webapps/] pasta.
1. Enviar uma solicitação para `https://localhost:8080/bees`.

   Se aparecer a mensagem &quot;O BEES está operacional&quot;, a implantação foi concluída com sucesso.
1. Habilite o SSL no servidor.
