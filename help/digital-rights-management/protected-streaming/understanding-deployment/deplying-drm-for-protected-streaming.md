---
title: Implantação do servidor DRM Adobe Primetime para transmissão protegida
description: Implantação do servidor DRM Adobe Primetime para transmissão protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Implantação do servidor DRM do Adobe Primetime para transmissão protegida{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Antes de implantar o Adobe Primetime DRM Server for Protected Streaming, é necessário instalar as versões do Java e Tomcat, conforme listado no tópico Requisitos.

O pacote Primetime DRM Server for Protected Streaming inclui [!DNL flashaccesserver.war]. Se você:

* Para implantar esse arquivo WAR, você precisa copiá-lo no diretório [!DNL webapps] do Tomcat.
* Depois de implantar o arquivo WAR anteriormente, talvez seja necessário excluir o diretório WAR descompactado ( [!DNL flashaccessserver] no diretório [!DNL webapps] do Tomcat).

* Deseja impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório [!DNL conf] do Tomcat e configure o atributo `unpackWARs` configurando-o para `false`.

>[!NOTE]
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no caminho da classe do sistema (não é necessário para o servidor DRM Primetime para transmissão protegida), é necessário configurar o registro de commons para usar o Log4J.

Opcionalmente, o servidor usa uma biblioteca específica da plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux para obter o melhor desempenho. Você pode copiar a biblioteca apropriada para sua plataforma de [!DNL thirdparty/cryptoj/]*platform* para um local especificado pela variável de ambiente `PATH` ou `LD_LIBRARY_PATH` no Linux.

>[!NOTE]
>
>Você só deve usar a versão de 64 bits se o sistema operacional e o JDK oferecerem suporte a 64 bits. Caso contrário, você precisará usar a versão de 32 bits.

