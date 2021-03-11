---
title: Visão geral do utilitário AIR Publisher ID
description: Visão geral do utilitário AIR Publisher ID
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Visão geral do utilitário AIR Publisher ID {#air-publisher-id-utility-overview}

Como parte do processo de criação de um arquivo do AIR, a Ferramenta de desenvolvedor do AIR (ADT) gera uma Publisher ID. Este é um identificador exclusivo do certificado usado para criar o arquivo do AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, eles terão a mesma Publisher ID. O utilitário AIR Publisher ID é usado para calcular a Publisher ID para um aplicativo AIR. As versões do AIR após 1.5.2 não gravam a Publisher ID gerada em um arquivo, portanto, é necessário usar essa ferramenta para determinar a Publisher ID se você estiver usando uma lista de permissões de aplicativo do AIR.

>[!NOTE]
>
>A Publisher ID, usada para a imposição da lista de permissões do AIR, não é a mesma que a Publisher ID especificada pelo publicador do aplicativo no arquivo [!DNL application.xml] do aplicativo.
