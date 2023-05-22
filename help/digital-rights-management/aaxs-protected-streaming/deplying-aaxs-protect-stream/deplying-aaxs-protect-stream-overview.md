---
title: Visão geral da implantação do Adobe Access Server para transmissão protegida
description: Visão geral da implantação do Adobe Access Server para transmissão protegida
copied-description: true
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Visão geral da implantação do Adobe Access Server para transmissão protegida {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implantar o Adobe Access Server para transmissão protegida, verifique se você instalou as versões do Java e do Tomcat listadas na seção Requisitos.

O pacote Adobe Access Server para Protected Streaming inclui [!DNL flashaccesserver.war]. Para implantar esse arquivo WAR, copie-o no do Tomcat [!DNL webapps] diretório. Se você tiver implantado anteriormente o arquivo WAR, talvez seja necessário excluir manualmente o diretório WAR desempacotado ( [!DNL flashaccessserver] no do Tomcat [!DNL webapps] diretório). Para evitar que o Tomcat descompacte arquivos WAR, edite o [!DNL server.xml] arquivo no do Tomcat [!DNL conf] e defina o `unpackWARs` atributo para `false`.

>[!NOTE]
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no caminho de classe Sistema (não necessário para o Adobe Access Server para transmissão protegida), o registro de commons deve ser configurado para usar o Log4J.

O servidor usa, opcionalmente, uma biblioteca específica de plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux) para obter o desempenho ideal. Copie a biblioteca apropriada para sua plataforma do [!DNL thirdparty/cryptoj/]*platform* para um local especificado pelo `PATH` variável de ambiente (ou `LD_LIBRARY_PATH` no Linux).

>[!NOTE]
>
>A versão de 64 bits só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits; caso contrário, use a versão de 32 bits.
