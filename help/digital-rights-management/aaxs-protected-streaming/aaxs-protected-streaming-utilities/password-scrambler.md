---
title: Scrambler de senhas
description: Scrambler de senhas
copied-description: true
exl-id: ceedd61e-918b-453f-8d21-628b2d8713ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
