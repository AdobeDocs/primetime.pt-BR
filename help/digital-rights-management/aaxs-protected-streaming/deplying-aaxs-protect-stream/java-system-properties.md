---
title: Propriedades do sistema Java
description: Propriedades do sistema Java
copied-description: true
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Propriedades do sistema Java {#java-system-properties}

As duas propriedades do sistema Java a seguir podem, opcionalmente, ser definidas para modificar o local dos arquivos de configuração e de registro do servidor de licenças:

* *LicenseServer.ConfigRoot* — Diretório contendo todos os arquivos de configuração do servidor de licenças. Para obter detalhes sobre o conteúdo desses arquivos, consulte &quot;[Arquivos de configuração do servidor de licenças](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Se não estiver definido, o padrão será *CATALINA_BASE/servidor de licenças*.
* *LicenseServer.LogRoot* — Diretório da pasta &quot;logs&quot;, onde os logs do aplicativo do servidor de licenças são gravados. Se não estiver definido, o padrão será *LicenseServer.ConfigRoot*.

Se você estiver usando [!DNL catalina.bat] ou [!DNL catalina.sh] para iniciar o Tomcat, essas propriedades do sistema podem ser facilmente definidas usando o `JAVA_OPTS` variável de ambiente. Quaisquer opções de Java definidas aqui serão usadas quando o Tomcat for iniciado. Por exemplo, defina:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
