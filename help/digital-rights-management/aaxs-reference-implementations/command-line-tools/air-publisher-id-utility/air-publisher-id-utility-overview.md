---
title: Visão geral do utilitário AIR Publisher ID
description: Visão geral do utilitário AIR Publisher ID
copied-description: true
exl-id: ad982ec8-0180-4185-8752-08592cabef3d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Visão geral do utilitário AIR Publisher ID {#air-publisher-id-utility-overview}

Como parte do processo de criação de um arquivo do AIR, a Ferramenta de desenvolvedor do AIR (ADT) gera uma ID do editor. É um identificador exclusivo do certificado usado para criar o arquivo do AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, eles terão a mesma ID do editor.O utilitário da ID do editor AIR é usado para calcular a ID do editor de um aplicativo AIR. As versões do AIR posteriores à 1.5.2 não gravam a ID do editor gerada em um arquivo. Portanto, é necessário usar essa ferramenta para determinar a ID do editor, se você estiver usando uma lista de permissões de aplicativo do AIR.

>[!NOTE]
>
>A ID do editor, usada para imposição de lista de permissões do AIR, não é a mesma que a ID do editor especificada pelo editor do aplicativo [!DNL application.xml] arquivo.
