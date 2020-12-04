---
seo-title: Criar a implementação de referência BEES
title: Criar a implementação de referência BEES
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Criar a implementação de referência do BEES {#build-the-bees-reference-implementation}

Verifique se você está usando o Java 1.6.0_24 ou posterior.
1. Preencha os caminhos vazios necessários, como `tomcatdir` e `fasterxmldir` em [!DNL build-bees.xml]

   XML/Jackson mais rápido está incluído. Você também pode baixá-lo de [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Atualize os nomes de arquivos jar reais em [!DNL build.common.xml] se quiser usar uma versão diferente das bibliotecas Jackson.
1. Execute o público alvo `all` de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

O [!DNL bees.war] será criado na pasta [!DNL bees-build/wars].