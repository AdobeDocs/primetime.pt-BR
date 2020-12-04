---
seo-title: Visão geral da implantação do Adobe Access Server para transmissão protegida
title: Visão geral da implantação do Adobe Access Server para transmissão protegida
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Implantação da visão geral do Adobe Access Server for Protected Streaming {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implantar o Adobe Access Server for Protected Streaming, verifique se você instalou as versões do Java e do Tomcat listadas na seção Requisitos.

O pacote Adobe Access Server for Protected Streaming inclui [!DNL flashaccesserver.war]. Para implantar esse arquivo WAR, copie-o no diretório [!DNL webapps] de Tomcat. Se você já implantou o arquivo WAR anteriormente, talvez seja necessário excluir manualmente o diretório WAR descompactado ( [!DNL flashaccessserver] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório [!DNL conf] do Tomcat e defina o atributo `unpackWARs` como `false`.

>[!NOTE]
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no classpath do sistema (não é necessário para o Adobe Access Server for Protected Streaming), o logon comum deve ser configurado para usar o Log4J.

Como opção, o servidor usa uma biblioteca específica da plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux) para obter o desempenho ideal. Copie a biblioteca apropriada para sua plataforma de [!DNL thirdparty/cryptoj/]*platform* para um local especificado pela variável de ambiente `PATH` (ou `LD_LIBRARY_PATH` no Linux).

>[!NOTE]
>
>A versão de 64 bits só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits, caso contrário use a versão de 32 bits.

