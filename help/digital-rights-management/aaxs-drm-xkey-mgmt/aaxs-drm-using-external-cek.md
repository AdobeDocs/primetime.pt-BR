---
description: Use o recurso CEK externo para vender e disponibilizar licenças usando seu CKMS existente.
seo-description: Use o recurso CEK externo para vender e disponibilizar licenças usando seu CKMS existente.
seo-title: Usando o CEK externo para Vend e as licenças do pacote
title: Usando o CEK externo para Vend e as licenças do pacote
uuid: 1bfd8c6c-4ae9-47de-8247-085b5360127d
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Usando o CEK externo para Vend e as licenças do pacote{#using-external-cek-to-vend-and-package-licenses}

Use o recurso CEK externo para vender e disponibilizar licenças usando seu CKMS existente.

## EncryptContentWithExternalKey.java

Esta é uma ferramenta de linha de comando que criptografará um vídeo pelo AAXS e criará metadados que *not* conterão o CEK (protegido pelo certificado público do servidor de licenças AAXS). Em vez disso, a ferramenta incorpora uma ID CEK nos metadados do vídeo.

Durante a aquisição da licença, o servidor de licença AAXS observa um sinalizador nos metadados que identifica que esse conteúdo foi protegido por meio de um CEK externo. O servidor de licenças extrairá a ID CEK dos metadados e, em seguida, fará o query de um repositório seguro/CKMS para recuperar o CEK apropriado.

## Fluxo de trabalho de empacotamento

1. Verifique se você está usando o Java 1.6.0_24 ou posterior.
1. Para ver o uso da ferramenta: `java -jar AdobePackager_ExternalCEK.jar`
1. Para empacotar conteúdo:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* O código-fonte Java pode ser criado usando o ANT `build-samples.xml` incluído
>* O SDK do Flash Access ( `adobe-flashaccess-sdk.jar`) deve estar no classpath

>



## Fluxo de trabalho do servidor

1. Configure a implementação de referência.
1. Se houver alguma, limpe as implantações anteriores de Implementação de referência:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verifique se há um arquivo [!DNL CEKDepot.properties] ao lado de [!DNL flashaccess-refimpl.properties]

1. Iniciar uma solicitação de licença de um Adobe Primetime Player
1. Observe os registros Ref Impl para obter algo semelhante a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Talvez seja necessário alterar suas configurações de [!DNL log4j.xml] para fazer logon em um nível `DEBUG` ( `INFO` está definido por padrão)

## Problemas conhecidos

Nenhum
