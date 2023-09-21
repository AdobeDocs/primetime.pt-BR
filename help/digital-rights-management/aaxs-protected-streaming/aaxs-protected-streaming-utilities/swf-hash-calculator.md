---
title: Calculadora de hash SWF
description: Calculadora de hash SWF
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# Calculadora de hash SWF{#swf-hash-calculator}

O utilitário Calculadora de hash de SWF calculou o resumo de um aplicativo SWF localizado em um arquivo. Para executar o hasher, execute o comando:

```
Hasher.bat filename.swf
```

ou o comando:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

O utilitário envia a seguinte mensagem:

```
SWF Hash: hash-of-swf
```

Este valor pode ser usado para especificar o resumo de SWF em [!DNL flashaccess-tenant.xml].
