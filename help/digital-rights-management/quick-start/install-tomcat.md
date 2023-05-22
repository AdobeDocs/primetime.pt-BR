---
title: Instalar Tomcat
description: Instalar Tomcat
copied-description: true
exl-id: aed8fc1c-0d75-47ca-bbd4-c0934a66e284
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Instalar Tomcat {#install-tomcat}

Você deve instalar o Tomcat em ambos os servidores.
1. Instale o Tomcat pelo [!DNL \Third Party\Tomcat\6.0.18\] no DVD de instalação.

   >[!NOTE]
   >
   >Certifique-se de que o Tomcat esteja instalado em um local onde não haja espaços no caminho. Você pode inserir `C:\Program Files\Tomcat`, mas não `C:\Tomcat\`.

1. Para iniciar o Tomcat, digite `TomcatInstallDir>\bin\catalina.bat run`.
1. Para verificar a instalação, vá para a página de aterrissagem do Tomcat inserindo `https://<Hostname>:8080/`.
1. Criar um `crossdomain.xml` e coloque o arquivo na caixa `<TomcatInstallDir>\webapps\ROOT\` diretório.

   Também é possível copiar um arquivo do `https://drmtest2.adobe.com/crossdomain.xml` diretório.
