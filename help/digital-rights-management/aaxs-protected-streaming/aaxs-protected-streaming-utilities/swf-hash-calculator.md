---
title: Calculadora de hash SWF
description: Calculadora de hash SWF
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
