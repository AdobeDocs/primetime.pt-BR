---
title: Criar a implementação de referência do BEES
description: Criar a implementação de referência do BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Criar a implementação de referência do BEES {#build-the-bees-reference-implementation}

Verifique se você está usando o Java 1.6.0_24 ou posterior.
1. Preencha os caminhos vazios necessários, como `tomcatdir` e `fasterxmldir` in [!DNL build-bees.xml]

   FasterXML/Jackson está incluído. Você também pode baixá-lo de [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Atualizar nomes de arquivo jar reais em [!DNL build.common.xml] se quiser usar uma versão diferente das bibliotecas Jackson.
1. Execute o `all` público alvo de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

A variável [!DNL bees.war] será criado na [!DNL bees-build/wars] pasta.
