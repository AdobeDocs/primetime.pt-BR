---
description: Há várias propriedades do Java System que você pode configurar no servidor de licenças para controlar o local da configuração e dos arquivos de log.
title: Propriedades do sistema Java
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Propriedades do sistema Java{#java-system-properties}

Há várias propriedades do Java System que você pode configurar no servidor de licenças para controlar o local da configuração e dos arquivos de log.

Opcionalmente, é possível configurar as seguintes propriedades do Sistema Java:

* *`LicenseServer.ConfigRoot`* — Nome do diretório que inclui os arquivos de configuração do servidor de licenças.

   Consulte *Arquivos de configuração do servidor de licença* para obter detalhes sobre o conteúdo desses arquivos. Se não estiver configurado, o valor padrão será `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot*  — Nome do  [!DNL logs] diretório em que os logs de aplicativos do servidor de licenças estão localizados. Se você não modificou o nome deste diretório, então o nome deste diretório é configurado como *LicenseServer.ConfigRoot* por padrão.

Se você usar o arquivo [!DNL catalina.bat] ou [!DNL catalina.sh] para iniciar o Tomcat, poderá configurar as Propriedades do sistema com a variável de ambiente `JAVA_OPTS`. Qualquer opção Java configurada é aplicada automaticamente quando o Tomcat é iniciado.

Por exemplo, você pode configurar a variável de ambiente `JAVA_OPTS` da seguinte maneira:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

