---
title: Verifique se o servidor de licenças foi iniciado corretamente
description: Verifique se o servidor de licenças foi iniciado corretamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Verifique se o servidor de licenças iniciou corretamente {#check-whether-the-license-server-started-properly}

Há várias maneiras de determinar se o Servidor de Licenças de Implementação de Referência foi iniciado corretamente. Uma maneira é verificar os registros [!DNL catalina.log], mas isso pode não ser suficiente, pois o servidor de licença faz logon em seus próprios arquivos de log.
1. Verifique o arquivo [!DNL AdobeFlashAccess.log].

   É aqui que o servidor de licença de Implementação de Referência grava informações de log. O local desse arquivo de log é indicado pelo seu arquivo [!DNL log4j.xml] e pode ser modificado para apontar para qualquer local. Por padrão, o arquivo de log é copiado para o diretório de trabalho onde você executa o script `catalina` Tomcat.
1. Vá para o seguinte URL e verifique se o texto &quot;O License Server está configurado corretamente&quot; é exibido:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
