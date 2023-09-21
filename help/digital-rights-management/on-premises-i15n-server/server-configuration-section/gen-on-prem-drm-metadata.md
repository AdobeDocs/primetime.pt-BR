---
title: Gerar os metadados de DRM no local
description: Gerar os metadados de DRM no local
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Gerar os metadados de DRM no local{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] O utilitário está incluído na [!DNL create_metadata] pasta. O objetivo desse utilitário é criar um Metadados DRM Local que iniciará o cliente na execução do processo de individualização em relação ao Servidor de individualização Local especificado.

1. Atualize a Implementação de referência de DRM do Primetime - Ferramentas de linha de comando com os seguintes arquivos:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

     Os dois arquivos JAR podem residir no [!DNL Command Line Tools/libs] pasta. A variável [!DNL createMetadata.properties] o arquivo pode ficar ao lado da [!DNL flashaccesstools.properties] arquivo.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Incluído é um [!DNL examplecreate.sh] script que demonstra uma amostra de criação de metadados. Certifique-se de configurar o URL do Servidor de licenças e o URL do Servidor de individualização nos arquivos de script e propriedades antes de tentar gerar metadados.

As entradas para o utilitário são as seguintes:

* `createMetadata.properties` - Arquivo de propriedades contendo uma política padrão, locais e senhas de certificados, etc.
* `indivCert` - Arquivo PKCS12 contendo certificado de Transporte de Individualização
* `indivURL` - URL do servidor de individualização local

O arquivo de saída é um arquivo de metadados DRM local que será consumido pelo cliente DRM. Por exemplo:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
