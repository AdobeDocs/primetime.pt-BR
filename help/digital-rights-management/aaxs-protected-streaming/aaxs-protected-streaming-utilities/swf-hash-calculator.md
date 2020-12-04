---
seo-title: Calculadora de hash SWF
title: Calculadora de hash SWF
uuid: c1823208-92d9-47c5-b550-f9cc370b543d
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Calculadora de hash SWF{#swf-hash-calculator}

O utilitário calculador de hash SWF calculou o resumo de um aplicativo SWF localizado em um arquivo. Para executar o hasher, execute o comando:

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
