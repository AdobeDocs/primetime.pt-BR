---
description: O utilitário Scrambler de senhas criptografa uma senha para o servidor DRM da Adobe Primetime para os arquivos de configuração de transmissão protegida.
title: Scrambler de senha
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Scrambler de senha {#password-scrambler}

O utilitário Scrambler de senhas criptografa uma senha para o servidor DRM da Adobe Primetime para os arquivos de configuração de transmissão protegida.

Para executar o scrambler, digite:

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

ou

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

O utilitário exibe a seguinte mensagem:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

Todas as senhas especificadas no [!DNL flashaccess-global.xml] e [!DNL flashaccess-tenant.xml] os arquivos devem ser criptografados.

>[!NOTE]
>
>O utilitário Scrambler de senhas no servidor DRM do Primetime para transmissão protegida não é intercambiável com o scrambler fornecido com o servidor de licenças de implementação de referência.
