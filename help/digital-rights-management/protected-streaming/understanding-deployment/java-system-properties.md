---
description: Existem várias propriedades do Java System que podem ser configuradas no servidor de licenças para controlar a localização dos arquivos de registro e configuração.
seo-description: Existem várias propriedades do Java System que podem ser configuradas no servidor de licenças para controlar a localização dos arquivos de registro e configuração.
seo-title: Propriedades do sistema Java
title: Propriedades do sistema Java
uuid: d8c72359-bf61-47e0-9cd5-b21225d5fe49
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Propriedades do sistema Java{#java-system-properties}

Existem várias propriedades do Java System que podem ser configuradas no servidor de licenças para controlar a localização dos arquivos de registro e configuração.

Opcionalmente, você pode configurar as seguintes propriedades do Java System:

* *`LicenseServer.ConfigRoot`* — Nome do diretório que inclui os arquivos de configuração do servidor de licenças.

   Consulte *Arquivos de configuração do servidor de licenças* para obter detalhes sobre o conteúdo desses arquivos. Se não estiver configurado, o valor padrão será `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Nome do  [!DNL logs] diretório no qual os logs de aplicativos do servidor de licenças estão localizados. Se você não modificou o nome desse diretório, o nome desse diretório será configurado como *LicenseServer.ConfigRoot* por padrão.

Se você usar o arquivo [!DNL catalina.bat] ou [!DNL catalina.sh] no start Tomcat, poderá configurar as propriedades do Sistema com a variável de ambiente `JAVA_OPTS`. Todas as opções Java configuradas são automaticamente aplicadas quando start Tomcat.

Por exemplo, você pode configurar a variável de ambiente `JAVA_OPTS` da seguinte maneira:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

