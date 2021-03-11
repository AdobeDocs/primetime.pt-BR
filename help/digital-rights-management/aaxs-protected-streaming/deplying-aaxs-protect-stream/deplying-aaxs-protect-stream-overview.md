---
title: Visão geral da implantação do Adobe Access Server para transmissão protegida
description: Visão geral da implantação do Adobe Access Server para transmissão protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Implantar o Adobe Access Server para visão geral de transmissão protegida {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implantar o Adobe Access Server for Protected Streaming, verifique se você instalou as versões do Java e Tomcat listadas na seção Requisitos .

O pacote Adobe Access Server for Protected Streaming inclui [!DNL flashaccesserver.war]. Para implantar esse arquivo WAR, copie-o no diretório [!DNL webapps] do Tomcat. Se você já implantou o arquivo WAR, talvez precise excluir manualmente o diretório WAR descompactado ( [!DNL flashaccessserver] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório [!DNL conf] do Tomcat e defina o atributo `unpackWARs` para `false`.

>[!NOTE]
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no caminho de classe do sistema (não é necessário para o Adobe Access Server para transmissão protegida), o registro em log do commons deve ser configurado para usar o Log4J.

Opcionalmente, o servidor usa uma biblioteca específica da plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux) para obter desempenho ideal. Copie a biblioteca apropriada para sua plataforma de [!DNL thirdparty/cryptoj/]*platform* para um local especificado pela variável de ambiente `PATH` (ou `LD_LIBRARY_PATH` no Linux).

>[!NOTE]
>
>A versão de 64 bits só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits, caso contrário, usarão a versão de 32 bits.

