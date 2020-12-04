---
description: O utilitário calculador de hash SWF calcula o resumo de um aplicativo SWF localizado em um arquivo.
seo-description: O utilitário calculador de hash SWF calcula o resumo de um aplicativo SWF localizado em um arquivo.
seo-title: Calculadora de hash SWF
title: Calculadora de hash SWF
uuid: 0cf972c1-4717-4d78-a594-b27178ece512
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Calculadora de hash SWF{#swf-hash-calculator}

O utilitário calculador de hash SWF calcula o resumo de um aplicativo SWF localizado em um arquivo.

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

Você pode usar esse valor para especificar o resumo SWF em [!DNL flashaccess-tenant.xml].
