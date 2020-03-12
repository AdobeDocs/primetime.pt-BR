---
seo-title: Instalar o Tomcat
title: Instalar o Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Instalar o Tomcat {#install-tomcat}

Você deve instalar o Tomcat em ambos os servidores.
1. Instale o Tomcat do diretório [!DNL \Third Party\Tomcat\6.0.18\] no DVD de instalação.

   >[!NOTE]
   >
   >Verifique se o Tomcat está instalado em um local onde não há espaços no caminho. Você pode entrar `C:\Program Files\Tomcat`, mas não `C:\Tomcat\`.

1. Para começar Tomcat, entre `TomcatInstallDir>\bin\catalina.bat run`.
1. Para verificar a instalação, vá para a página de aterrissagem do Tomcat digitando `https://<Hostname>:8080/`.
1. Crie um `crossdomain.xml` arquivo e coloque-o no `<TomcatInstallDir>\webapps\ROOT\` diretório.

   Você também pode copiar um arquivo do `https://drmtest2.adobe.com/crossdomain.xml` diretório.
