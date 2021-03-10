---
description: Se quiser configurar o DRM do Primetime, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, você precisa solicitar um certificado da Adobe Systems, Incorporated. O Adobe então emite várias credenciais que você usa para proteger a integridade de seu conteúdo empacotado, licenças e comunicação entre o cliente e o servidor.
title: Configurar o ambiente de desenvolvimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Configurar o ambiente de desenvolvimento {#set-up-your-development-environment}

Se quiser configurar o DRM do Primetime, copie os arquivos do DVD. Esses arquivos incluem arquivos JAR que incluem código, certificados e classes de terceiros. Além disso, você precisa solicitar um certificado da Adobe Systems, Incorporated. O Adobe então emite várias credenciais que você usa para proteger a integridade de seu conteúdo empacotado, licenças e comunicação entre o cliente e o servidor.

O Adobe fornece o SDK de DRM do Primetime em DVD:

1. Copie os seguintes arquivos de [!DNL [DRM DVD]/SDK/] para seu sistema de desenvolvimento (no caminho de classe Java):

   * [!DNL adobe-flashaccess-certs.jar] - Inclui certificados Adobe root
   * [!DNL adobe-flashaccess-sdk.jar] - Inclui classes SDK principais de DRM do Primetime
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Inclui as classes SDK do Primetime DRM Professional, necessárias apenas para recursos Professional

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

1. (Opcional) Para melhorar o desempenho, é possível habilitar o suporte nativo para operações criptográficas copiando a biblioteca específica da plataforma apropriada do [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] para o seu sistema de desenvolvimento (lembre-se de colocar o local no seu caminho):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >As versões de 32 bits e 64 bits dessas bibliotecas estão disponíveis. Você só deve usar a versão de 64 bits se tiver um SO de 64 bits e executar a versão de 64 bits do Java.

1. (Opcional) Para a funcionalidade relacionada à compatibilidade do Adobe Flash Media Rights Management Server (FMRMS) 1.x, copie `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` para o sistema de desenvolvimento:

   Implante isso somente se tiver implantado anteriormente o FMRMS 1.x e não quiser reempacotar seu conteúdo protegido por FMRMS. Nesse caso, você deve adicionar esse suporte ao seu servidor de licenças para que ele possa gerenciar conteúdo e clientes antigos.
