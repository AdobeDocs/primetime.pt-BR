---
description: Há várias propriedades do Java System que você pode configurar no servidor de licenças para controlar o local dos arquivos de configuração e log.
title: Propriedades do sistema Java
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Propriedades do sistema Java{#java-system-properties}

Há várias propriedades do Java System que você pode configurar no servidor de licenças para controlar o local dos arquivos de configuração e log.

Opcionalmente, é possível configurar as seguintes propriedades do sistema Java:

* *`LicenseServer.ConfigRoot`* — Nome do diretório que inclui os arquivos de configuração do servidor de licenças.

   Consulte *Arquivos de configuração do servidor de licenças* para obter detalhes sobre o conteúdo desses arquivos. Se não estiver configurado, o valor padrão será `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Nome do [!DNL logs] diretório no qual os logs de aplicativo do servidor de licenças estão localizados. Se você não tiver modificado o nome desse diretório, ele será configurado como *LicenseServer.ConfigRoot* por padrão.

Se você usar o [!DNL catalina.bat] ou [!DNL catalina.sh] para iniciar o Tomcat, você pode configurar as propriedades do sistema com a variável `JAVA_OPTS` variável de ambiente. Qualquer opção Java configurada é automaticamente aplicada quando o Tomcat é iniciado.

Por exemplo, você pode configurar a variável `JAVA_OPTS` variável de ambiente da seguinte maneira:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
