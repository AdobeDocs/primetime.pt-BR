---
seo-title: Visão geral do utilitário da ID do editor do AIR
title: Visão geral do utilitário da ID do editor do AIR
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visão geral do utilitário da ID do editor do AIR {#air-publisher-id-utility-overview}

Como parte do processo de criação de um arquivo AIR, a AIR Developer Tool (ADT) gera uma Publisher ID. Este é um identificador exclusivo do certificado usado para criar o arquivo AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, eles terão a mesma Publisher ID. O utilitário AIR Publisher ID é usado para calcular a Publisher ID para um aplicativo AIR. As versões do AIR após 1.5.2 não gravam a Publisher ID gerada em um arquivo, portanto, é necessário usar essa ferramenta para determinar a Publisher ID se você estiver usando uma lista de permissões do aplicativo AIR.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A Publisher ID, usada para a imposição da lista de permissões do AIR, não é a mesma ID do Publisher especificada pelo editor do aplicativo no [!DNL application.xml] arquivo do aplicativo.

