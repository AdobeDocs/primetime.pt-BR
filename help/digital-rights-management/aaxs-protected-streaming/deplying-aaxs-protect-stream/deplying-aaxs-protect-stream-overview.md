---
seo-title: Implantação da visão geral do Adobe Access Server for Protected Streaming
title: Implantação da visão geral do Adobe Access Server for Protected Streaming
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Implantação da visão geral do Adobe Access Server for Protected Streaming {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Antes de implantar o Adobe Access Server for Protected Streaming, verifique se você instalou as versões do Java e do Tomcat listadas na seção Requisitos.

O pacote Adobe Access Server for Protected Streaming inclui [!DNL flashaccesserver.war]. Para implantar esse arquivo WAR, copie-o no [!DNL webapps] diretório do Tomcat. Se você tiver implantado o arquivo WAR anteriormente, talvez seja necessário excluir manualmente o diretório WAR descompactado ( [!DNL flashaccessserver] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o [!DNL server.xml] arquivo no diretório [!DNL conf] do Tomcat e defina o `unpackWARs` atributo como `false`.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Se você configurou o Tomcat para incluir [!DNL commons-logging.jar] no classpath do sistema (não é necessário para o Adobe Access Server for Protected Streaming), o logon comum deverá ser configurado para usar o Log4J.

Como opção, o servidor usa uma biblioteca específica da plataforma ( [!DNL jsafe.dll] no Microsoft Windows ou [!DNL libjsafe.so] no Linux) para obter o desempenho ideal. Copie a biblioteca apropriada para sua plataforma da [!DNL thirdparty/cryptoj/]*plataforma *para um local especificado pela variável de`PATH`ambiente (ou`LD_LIBRARY_PATH`no Linux).

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A versão de 64 bits só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits, caso contrário use a versão de 32 bits.

