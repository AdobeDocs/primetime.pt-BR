---
seo-title: Gerar os metadados DRM locais
title: Gerar os metadados DRM locais
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Gerar os metadados de DRM locais{#generate-the-on-premises-drm-metadata}

Um utilitário [!DNL CreateMetadata.jar] está incluído na pasta [!DNL create_metadata]. O objetivo deste utilitário é criar um Metadados de DRM locais que iniciarão o cliente a executar o processo de individualização em relação ao servidor de individualização local especificado.

1. Atualize a implementação de referência do Primetime DRM - Ferramentas de linha de comando com os seguintes arquivos:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      Os dois arquivos JAR podem residir na pasta [!DNL Command Line Tools/libs]. O arquivo [!DNL createMetadata.properties] pode residir ao lado do arquivo [!DNL flashaccesstools.properties].

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Inclui um script [!DNL examplecreate.sh] que demonstra uma amostra da criação de metadados. Certifique-se de configurar o URL do servidor de licença e o URL do servidor de individualização nos arquivos de script e propriedades antes de tentar gerar metadados.

As entradas do utilitário são as seguintes:

* `createMetadata.properties` - Arquivo de propriedades que contém uma política padrão, locais de certificados e senhas, etc.
* `indivCert` - Arquivo PKCS12 contendo o certificado de Transporte de individualização
* `indivURL` - URL do servidor de diferenciação local

O arquivo de saída é um arquivo de metadados DRM locais que será consumido pelo cliente DRM. Por exemplo:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.