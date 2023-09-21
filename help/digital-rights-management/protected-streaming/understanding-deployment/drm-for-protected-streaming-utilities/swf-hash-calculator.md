---
description: O utilitário Calculadora de hash de SWF calcula o resumo de um aplicativo SWF que está localizado em um arquivo.
title: calculadora de hash SWF
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# calculadora de hash SWF{#swf-hash-calculator}

O utilitário Calculadora de hash de SWF calcula o resumo de um aplicativo SWF que está localizado em um arquivo.

Para executar o hasher, digite:

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

ou

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

O utilitário exibe a seguinte mensagem:

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

Você pode usar esse valor para especificar o resumo de SWF em [!DNL flashaccess-tenant.xml].
