---
title: Calculadora de hash SWF
description: Calculadora de hash SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Calculadora de hash SWF{#swf-hash-calculator}

O utilitário Calculadora de Hash SWF calculou o resumo de um aplicativo SWF localizado em um arquivo. Para executar o hash, execute o comando:

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

Esse valor pode ser usado para especificar o resumo SWF em [!DNL flashaccess-tenant.xml].
