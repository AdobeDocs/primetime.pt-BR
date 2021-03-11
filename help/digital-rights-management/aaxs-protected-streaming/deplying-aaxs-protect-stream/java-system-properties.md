---
title: Propriedades do sistema Java
description: Propriedades do sistema Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Propriedades do sistema Java {#java-system-properties}

Como opção, as duas propriedades do Java System a seguir podem ser definidas para modificar o local da configuração e dos arquivos de log do servidor de licença:

* *LicenseServer.ConfigRoot*  — Diretório contendo todos os arquivos de configuração do servidor de licenças. Para obter detalhes sobre o conteúdo desses arquivos, consulte &quot;[Arquivos de configuração do servidor de licença](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Se não estiver definido, o padrão será *CATALINA_BASE/licencieserver*.
* *LicenseServer.LogRoot*  — Diretório da pasta &quot;logs&quot;, onde os logs de aplicativos do servidor de licenças são gravados. Se não estiver definido, o padrão será *LicenseServer.ConfigRoot*.

Se você estiver usando [!DNL catalina.bat] ou [!DNL catalina.sh] para iniciar o Tomcat, essas propriedades do sistema poderão ser facilmente definidas usando a variável de ambiente `JAVA_OPTS`. Qualquer opção Java definida aqui será usada quando o Tomcat for iniciado. Por exemplo, defina:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

