---
description: O utilitário Scrambler de senha criptografa uma senha para o Adobe Primetime DRM Server para arquivos de configuração de transmissão protegidos.
title: Senha
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Senha de script {#password-scrambler}

O utilitário Scrambler de senha criptografa uma senha para o Adobe Primetime DRM Server para arquivos de configuração de transmissão protegidos.

Para executar o script, digite:

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

Todas as senhas especificadas nos arquivos [!DNL flashaccess-global.xml] e [!DNL flashaccess-tenant.xml] devem ser criptografadas.

>[!NOTE]
>
>O utilitário Scrambler de senha no servidor DRM Primetime para transmissão protegida não é intercambiável com o sambler fornecido com o Servidor de licença de implementação de referência.