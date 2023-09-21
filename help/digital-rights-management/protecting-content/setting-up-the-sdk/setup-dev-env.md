---
description: Se quiser configurar o Primetime DRM, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, você precisa solicitar um certificado da Adobe Systems, Incorporated. O Adobe emite várias credenciais usadas para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.
title: Configurar o ambiente de desenvolvimento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Configurar o ambiente de desenvolvimento {#set-up-your-development-environment}

Se quiser configurar o Primetime DRM, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, você precisa solicitar um certificado da Adobe Systems, Incorporated. O Adobe emite várias credenciais usadas para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.

O Adobe fornece o SDK DRM do Primetime em DVD:

1. Copiar os arquivos a seguir do [!DNL [DVD DRM]/SDK/] para o seu sistema de desenvolvimento (no classpath do Java):

   * [!DNL adobe-flashaccess-certs.jar] - Inclui certificados raiz de Adobe
   * [!DNL adobe-flashaccess-sdk.jar] - Inclui as classes de SDK principal DRM do Primetime
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Inclui as classes de SDK profissional DRM do Primetime, necessárias apenas para recursos profissionais

1. Copiar os arquivos a seguir do [!DNL [DVD DRM]/SDK/thirdparty] para o seu sistema de desenvolvimento:

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (Opcional) Para melhorar o desempenho, você pode habilitar o suporte nativo para operações de criptografia copiando a biblioteca específica da plataforma apropriada do [!DNL [DVD DRM]/SDK/thirdparty/cryptoj/] para o seu sistema de desenvolvimento (lembre-se de colocar o local no caminho):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

     >[!NOTE]
     >
     >As versões de 32 bits e 64 bits dessas bibliotecas estão disponíveis. Você só deve usar a versão de 64 bits se tiver um SO de 64 bits e executar a versão de 64 bits do Java.

1. (Opcional) Para obter a funcionalidade relacionada à compatibilidade do Adobe Flash Media Rights Management Server (FMRMS) 1.x, copie `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` ao seu sistema de desenvolvimento:

   Implante somente se tiver implantado anteriormente o FMRMS 1.x e não quiser empacotar novamente o conteúdo protegido por FMRMS. Nesse caso, você deve adicionar esse suporte ao servidor de licenças para que ele possa gerenciar conteúdo e clientes antigos.
