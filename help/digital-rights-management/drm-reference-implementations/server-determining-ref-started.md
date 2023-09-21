---
title: Verifique se o servidor de licenças foi iniciado corretamente
description: Verifique se o servidor de licenças foi iniciado corretamente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Verifique se o servidor de licenças foi iniciado corretamente {#check-whether-the-license-server-started-properly}

Há várias maneiras de determinar se o Servidor de licenças de implementação de referência foi iniciado corretamente. Uma maneira é verificar a [!DNL catalina.log] registros, mas isso pode não ser suficiente, pois o servidor de licenças registra seus próprios arquivos de log.
1. Verifique o seu [!DNL AdobeFlashAccess.log] arquivo.

   É aqui que o servidor de licenças de Implementação de referência grava informações de log. O local desse arquivo de log é indicado pelo seu [!DNL log4j.xml] e podem ser modificadas para apontar para qualquer local. Por padrão, o arquivo de log é copiado para o diretório de trabalho onde você executa o `catalina` Script do Tomcat.
1. Vá para o seguinte URL e verifique se o texto &quot;License Server is setup correctly&quot; (O servidor de licenças está configurado corretamente) é exibido:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
