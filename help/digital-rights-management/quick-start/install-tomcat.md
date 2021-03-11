---
title: Instalar o Tomcat
description: Instalar o Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Instalar o Tomcat {#install-tomcat}

Você deve instalar o Tomcat em ambos os servidores.
1. Instale o Tomcat no diretório  [!DNL \Third Party\Tomcat\6.0.18\] no DVD de instalação.

   >[!NOTE]
   >
   >Verifique se o Tomcat está instalado em um local onde não há espaços no caminho. Você pode inserir `C:\Program Files\Tomcat`, mas não `C:\Tomcat\`.

1. Para iniciar o Tomcat, digite `TomcatInstallDir>\bin\catalina.bat run`.
1. Para verificar a instalação, vá para a página de aterrissagem do Tomcat digitando `https://<Hostname>:8080/`.
1. Crie um arquivo `crossdomain.xml` e coloque-o no diretório `<TomcatInstallDir>\webapps\ROOT\`.

   Você também pode copiar um arquivo do diretório `https://drmtest2.adobe.com/crossdomain.xml`.
