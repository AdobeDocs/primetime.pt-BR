---
title: Criar a implementação de referência do BEES
description: Criar a implementação de referência do BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Criar a implementação de referência BEES {#build-the-bees-reference-implementation}

Verifique se você está usando o Java 1.6.0_24 ou posterior.
1. Preencha os caminhos vazios necessários, como `tomcatdir` e `fasterxmldir` em [!DNL build-bees.xml]

   FasterXML/Jackson é incluído. Também é possível baixá-lo em [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Atualize os nomes de arquivo jar reais em [!DNL build.common.xml] se desejar usar uma versão diferente das bibliotecas Jackson.
1. Execute o destino `all` de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

O [!DNL bees.war] será criado na pasta [!DNL bees-build/wars].