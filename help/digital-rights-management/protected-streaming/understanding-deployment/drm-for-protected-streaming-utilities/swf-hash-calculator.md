---
description: O utilitário Calculadora de Hash SWF calcula o resumo de um aplicativo SWF localizado em um arquivo.
title: Calculadora de hash SWF
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# Calculadora de hash SWF{#swf-hash-calculator}

O utilitário Calculadora de Hash SWF calcula o resumo de um aplicativo SWF localizado em um arquivo.

Para executar o hash, digite:

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

Você pode usar esse valor para especificar o resumo SWF em [!DNL flashaccess-tenant.xml].
