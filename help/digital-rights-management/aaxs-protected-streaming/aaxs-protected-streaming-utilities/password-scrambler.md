---
title: Scrambler de senhas
description: Scrambler de senhas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Scrambler de senhas {#password-scrambler}

O utilitário Scrambler de senhas criptografa uma senha para que ela possa ser usada no Adobe Access Server para arquivos de configuração de transmissão protegida. Para executar o scrambler, execute o comando:

```
Scrambler.bat password 
```

ou o comando:

```
java -jar libs/flashaccess-scrambler.jar password  
```

O utilitário emite a seguinte mensagem:

```
Encrypted password: scrambled-password 
```

Todas as senhas especificadas em flashaccess-global.xml e flashaccess-tenant.xml devem ser criptografadas.

>[!NOTE]
>
>O utilitário Scrambler de senhas no Adobe Access Server para transmissão protegida não é intercambiável com o scrambler fornecido com o servidor de licenças de implementação de referência.
