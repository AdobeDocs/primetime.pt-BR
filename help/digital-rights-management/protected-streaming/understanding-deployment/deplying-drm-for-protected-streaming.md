---
seo-title: Implantação do Adobe Primetime DRM Server para streaming protegido
title: Implantação do Adobe Primetime DRM Server para streaming protegido
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Implantação do Adobe Primetime DRM Server para streaming protegido{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Antes de implantar o Adobe Primetime DRM Server for Protected Streaming, você deve ter instalado as versões do Java e do Tomcat, conforme listado no tópico Requisitos.

O pacote Primetime DRM Server for Protected Streaming inclui [!DNL flashaccesserver.war]. Se você:

* Deseja implantar este arquivo WAR, é necessário copiá-lo para o [!DNL webapps] diretório do Tomcat.
* Se o arquivo WAR tiver sido implantado anteriormente, talvez seja necessário excluir o diretório WAR descompactado ( [!DNL flashaccessserver] no diretório [!DNL webapps] do Tomcat).

* Deseja impedir que o Tomcat descompacte arquivos WAR, edite o arquivo no [!DNL server.xml] diretório do Tomcat [!DNL conf] e configure o `unpackWARs` atributo definindo-o como `false`.

>[!NOTE]
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no classpath do sistema (não é necessário para o servidor DRM Primetime para streaming protegido), é necessário configurar o logon comum para usar o Log4J.

Como opção, o servidor usa uma biblioteca específica da plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux) para obter o desempenho ideal. Você pode copiar a biblioteca apropriada para sua plataforma, da [!DNL thirdparty/cryptoj/]*plataforma *para um local especificado pela variável do`PATH`ambiente ou`LD_LIBRARY_PATH`no Linux.

>[!NOTE]
>
>Você só deve usar a versão de 64 bits se o sistema operacional e o JDK oferecerem suporte a 64 bits. Caso contrário, será necessário usar a versão de 32 bits.

