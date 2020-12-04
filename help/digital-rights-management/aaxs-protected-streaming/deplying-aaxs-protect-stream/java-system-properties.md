---
seo-title: Propriedades do sistema Java
title: Propriedades do sistema Java
uuid: ad1f3d9b-7d95-4e19-a0f8-fd7d4dd4dc32
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Propriedades do sistema Java {#java-system-properties}

Como opção, as duas propriedades do Java System podem ser definidas para modificar o local dos arquivos de configuração e registro do servidor de licenças:

* *LicenseServer.ConfigRoot* — Diretório que contém todos os arquivos de configuração do servidor de licenças. Para obter detalhes sobre o conteúdo desses arquivos, consulte &quot;[Arquivos de configuração do servidor de licença](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Se não estiver definido, o padrão será *CATALINA_BASE/licencieserver*.
* *LicenseServer.LogRoot* — Diretório da pasta &quot;logs&quot;, onde os logs de aplicativos do servidor de licenças são gravados. Se não estiver definido, o padrão será *LicenseServer.ConfigRoot*.

Se você estiver usando [!DNL catalina.bat] ou [!DNL catalina.sh] para o start Tomcat, essas propriedades do sistema podem ser facilmente definidas usando a variável de ambiente `JAVA_OPTS`. Qualquer opção Java definida aqui será usada quando o Tomcat for iniciado. Por exemplo, defina:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

