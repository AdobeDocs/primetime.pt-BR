---
description: Use o recurso CEK externo para fornecer e empacotar licenças usando seu CKMS existente.
title: Uso do CEK externo para venda e empacotamento de licenças
exl-id: 3944624a-099e-4fc0-b829-6ab154a53758
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Uso do CEK externo para venda e empacotamento de licenças{#using-external-cek-to-vend-and-package-licenses}

Use o recurso CEK externo para fornecer e empacotar licenças usando seu CKMS existente.

## EncryptContentWithExternalKey.java

Esta é uma ferramenta de linha de comando que criptografará um vídeo com AXS e criará metadados que *não* contém o CEK (protegido com um certificado público do servidor de licenças AXS). Em vez disso, a ferramenta incorpora uma ID do CEK nos metadados do vídeo.

Durante a aquisição da licença, o servidor de licenças AXS observa um sinalizador nos metadados identificando que esse conteúdo foi protegido usando um CEK externo. O servidor de licenças extrairá a ID do CEK dos metadados e consultará um repositório seguro/CKMS para recuperar o CEK apropriado.

## Fluxo de trabalho de empacotamento

1. Verifique se você está usando o Java 1.6.0_24 ou posterior.
1. Para ver o uso da ferramenta: `java -jar AdobePackager_ExternalCEK.jar`
1. Para compactar o conteúdo:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* O código-fonte Java pode ser construído usando o ANT incluído `build-samples.xml`
>* O SDK do Flash Access ( `adobe-flashaccess-sdk.jar`) deve estar no classpath
>


## Fluxo de trabalho do servidor

1. Configure a Implementação de referência.
1. Se houver, limpe as implantações anteriores da Implementação de referência:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verifique se há uma [!DNL CEKDepot.properties] arquivo junto com seu [!DNL flashaccess-refimpl.properties]

1. Iniciar uma solicitação de licença de um Adobe Primetime Player
1. Observe registros de Impl de referência para algo semelhante a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Talvez seja necessário alterar o [!DNL log4j.xml] configurações para registrar em um `DEBUG` nível ( `INFO` é definido por padrão)

## Problemas conhecidos

Nenhum
