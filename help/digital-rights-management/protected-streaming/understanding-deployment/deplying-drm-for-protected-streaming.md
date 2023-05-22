---
title: Implantação do servidor DRM do Adobe Primetime para transmissão protegida
description: Implantação do servidor DRM do Adobe Primetime para transmissão protegida
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Implantação do servidor DRM do Adobe Primetime para transmissão protegida{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Antes de implantar o servidor DRM da Adobe Primetime para transmissão protegida, você deve ter instalado as versões do Java e do Tomcat conforme listado no tópico Requisitos.

O pacote do servidor DRM Primetime para Transmissão protegida inclui [!DNL flashaccesserver.war]. Se você:

* Para implantar esse arquivo WAR, é necessário copiá-lo para o do Tomcat [!DNL webapps] diretório.
* Ter implantado anteriormente o arquivo WAR, talvez seja necessário excluir o diretório WAR desempacotado ( [!DNL flashaccessserver] no do Tomcat [!DNL webapps] diretório).

* Para evitar que o Tomcat descompacte arquivos WAR, edite o [!DNL server.xml] arquivo no do Tomcat [!DNL conf] e configure o `unpackWARs` atributo ao configurá-lo como `false`.

>[!NOTE]
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no caminho de classe Sistema (não necessário para o Servidor DRM do Primetime para Transmissão protegida), você deve configurar o registro commons para usar o Log4J.

O servidor usa, opcionalmente, uma biblioteca específica de plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux para obter o desempenho ideal. Você pode copiar a biblioteca apropriada para sua plataforma do [!DNL thirdparty/cryptoj/]*platform* para um local especificado pelo `PATH` variável de ambiente ou `LD_LIBRARY_PATH` no Linux.

>[!NOTE]
>
>Você só deve usar a versão de 64 bits se o sistema operacional e o JDK forem compatíveis com 64 bits. Caso contrário, você precisará usar a versão de 32 bits.
