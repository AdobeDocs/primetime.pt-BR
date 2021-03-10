---
title: Gerar os metadados de DRM locais
description: Gerar os metadados de DRM locais
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Gerar os metadados de DRM locais{#generate-the-on-premises-drm-metadata}

Um utilitário [!DNL CreateMetadata.jar] está incluído na pasta [!DNL create_metadata]. O objetivo desse utilitário é criar um Metadado de DRM no local que iniciará o cliente para executar o processo de individualização em relação ao Servidor de individualização no local especificado.

1. Atualize a implementação de referência do Primetime DRM - Ferramentas de linha de comando com os seguintes arquivos:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      Os dois arquivos JAR podem residir na pasta [!DNL Command Line Tools/libs]. O arquivo [!DNL createMetadata.properties] pode residir ao lado do arquivo [!DNL flashaccesstools.properties].

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Incluído é um script [!DNL examplecreate.sh] que demonstra uma criação de amostra de metadados. Certifique-se de configurar o URL do License Server e o URL do Servidor de Individualização nos arquivos de script e propriedades antes de tentar gerar metadados.

As entradas para o utilitário são as seguintes:

* `createMetadata.properties` - Arquivo de propriedades contendo uma Política padrão, locais de certificados e senhas, etc.
* `indivCert` - Arquivo PKCS12 contendo certificado de transporte de individualização
* `indivURL` - URL do servidor de individualização no local

O arquivo de saída é um arquivo de metadados DRM nas instalações que será consumido pelo cliente DRM. Por exemplo:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.