---
description: Se quiser configurar o DRM Primetime, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, é necessário solicitar um certificado da Adobe Systems, Incorporated. Em seguida, a Adobe emite várias credenciais que você usa para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.
seo-description: Se quiser configurar o DRM Primetime, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, é necessário solicitar um certificado da Adobe Systems, Incorporated. Em seguida, a Adobe emite várias credenciais que você usa para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.
seo-title: Configurar seu ambiente de desenvolvimento
title: Configurar seu ambiente de desenvolvimento
uuid: 68afefe8-7ec6-466e-89a8-bc0da8afb4c8
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Configurar seu ambiente de desenvolvimento {#set-up-your-development-environment}

Se quiser configurar o DRM Primetime, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, é necessário solicitar um certificado da Adobe Systems, Incorporated. Em seguida, a Adobe emite várias credenciais que você usa para proteger a integridade do conteúdo empacotado, das licenças e da comunicação entre o cliente e o servidor.

A Adobe fornece o SDK do DRM Primetime em DVD:

1. Copie os seguintes arquivos do [!DNL [DRM DVD]/SDK/] para o sistema de desenvolvimento (no caminho de classe Java):

   * [!DNL adobe-flashaccess-certs.jar] - Inclui certificados raiz da Adobe
   * [!DNL adobe-flashaccess-sdk.jar] - Inclui classes SDK principais do Primetime DRM
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Inclui classes SDK do Primetime DRM Professional, necessárias somente para recursos Professional

1. Copie os seguintes arquivos de [!DNL [DRM DVD]/SDK/thirdparty] para o seu sistema de desenvolvimento:

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

1. (Opcional) Para melhorar o desempenho, você pode habilitar o suporte nativo para operações criptográficas copiando a biblioteca específica da plataforma apropriada de [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] para o seu sistema de desenvolvimento (lembre-se de colocar o local no caminho):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >As versões de 32 bits e 64 bits dessas bibliotecas estão disponíveis. Você só deve usar a versão de 64 bits se tiver um SO de 64 bits e executar a versão de 64 bits do Java.

1. (Opcional) Para a funcionalidade relacionada à compatibilidade do Adobe Flash Media Rights Management Server (FMRMS) 1.x, copie `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` para o seu sistema de desenvolvimento:

   Implante isso somente se você implantou o FMRMS 1.x anteriormente e não quiser empacotar novamente seu conteúdo protegido por FMRMS. Nesse caso, você deve adicionar esse suporte ao seu servidor de licenças para que ele possa gerenciar conteúdo e clientes antigos.
