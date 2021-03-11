---
title: Scrambler Senha
description: Scrambler Senha
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Scrambler de senha {#password-scrambler}

O utilitário Scrambler de senha criptografa uma senha para que ela possa ser usada no Adobe Access Server para arquivos de configuração de fluxo protegido. Para executar o script, execute o comando:

```
Scrambler.bat password 
```

ou o comando:

```
java -jar libs/flashaccess-scrambler.jar password  
```

O utilitário gera a seguinte mensagem:

```
Encrypted password: scrambled-password 
```

Todas as senhas especificadas em flashaccess-global.xml e flashaccess-tenant.xml devem ser criptografadas.

>[!NOTE]
>
>O utilitário Scrambler de senha no Adobe Access Server for Protected Streaming não é intercambiável com o sambler fornecido com o Servidor de licença de implementação de referência.

