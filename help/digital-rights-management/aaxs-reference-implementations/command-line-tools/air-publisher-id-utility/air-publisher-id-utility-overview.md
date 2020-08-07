---
seo-title: Visão geral do utilitário da ID do editor do AIR
title: Visão geral do utilitário da ID do editor do AIR
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Visão geral do utilitário da ID do editor do AIR {#air-publisher-id-utility-overview}

Como parte do processo de criação de um arquivo AIR, a AIR Developer Tool (ADT) gera uma Publisher ID. Este é um identificador exclusivo do certificado usado para criar o arquivo AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, eles terão a mesma Publisher ID. O utilitário AIR Publisher ID é usado para calcular a Publisher ID para um aplicativo AIR. As versões do AIR após 1.5.2 não gravam a Publisher ID gerada em um arquivo, portanto, é necessário usar essa ferramenta para determinar a Publisher ID se você estiver usando uma lista de permissões de aplicativo do AIR.

>[!NOTE]
>
>A ID do editor, usada para a imposição de lista de permissões do AIR, não é a mesma ID do editor especificada pelo editor do aplicativo no [!DNL application.xml] arquivo do aplicativo.
