---
title: Implantar a implementação de referência do BEES
description: Implantar a implementação de referência do BEES
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
