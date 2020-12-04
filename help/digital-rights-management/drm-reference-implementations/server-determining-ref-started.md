---
description: nulo
seo-description: nulo
seo-title: Verifique se o servidor de licenças foi iniciado corretamente
title: Verifique se o servidor de licenças foi iniciado corretamente
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Verifique se o servidor de licenças foi iniciado corretamente {#check-whether-the-license-server-started-properly}

Existem várias maneiras de determinar se o Servidor de Licenças de Implementação de Referência foi iniciado corretamente. Uma maneira é verificar os registros [!DNL catalina.log], mas isso pode não ser suficiente, já que o servidor de licenças faz logon em seus próprios arquivos de log.
1. Verifique seu arquivo [!DNL AdobeFlashAccess.log].

   É aqui que o servidor de licença de Implementação de Referência grava informações de log. O local desse arquivo de log é indicado pelo arquivo [!DNL log4j.xml] e pode ser modificado para apontar para qualquer local. Por padrão, o arquivo de log é copiado para o diretório de trabalho onde você executa o script `catalina` do Tomcat.
1. Vá para o seguinte URL e verifique se o texto &quot;License Server is setup correctly&quot; (O servidor de licença está configurado corretamente) é exibido:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
