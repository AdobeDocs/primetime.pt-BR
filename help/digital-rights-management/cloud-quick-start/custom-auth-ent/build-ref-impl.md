---
seo-title: Criar a implementação de referência BEES
title: Criar a implementação de referência BEES
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Criar a implementação de referência BEES {#build-the-bees-reference-implementation}

Verifique se você está usando o Java 1.6.0_24 ou posterior.
1. Preencha os caminhos vazios necessários, como `tomcatdir` e `fasterxmldir` em [!DNL build-bees.xml]

   XML/Jackson mais rápido está incluído. Você também pode baixá-lo em [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Atualize os nomes dos arquivos jar reais em [!DNL build.common.xml] caso deseje usar uma versão diferente das bibliotecas Jackson.
1. Execute o `all` destino de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

A pasta [!DNL bees.war] será criada na [!DNL bees-build/wars] pasta.