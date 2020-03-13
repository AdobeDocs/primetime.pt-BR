---
seo-title: Scrambler de senha
title: Scrambler de senha
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Scrambler de senha {#password-scrambler}

O utilitário Scrambler de senha criptografa uma senha para que ela possa ser usada no Adobe Access Server para arquivos de configuração de streaming protegidos. Para executar o script, execute o comando:

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

Todas as senhas especificadas em flashaccess-global.xml e flashaccess-locatário.xml devem ser criptografadas.

>[!NOTE]
>
>O utilitário Scrambler de senha no Adobe Access Server for Protected Streaming não é intercambiável com o sambler fornecido com o Servidor de licença de implementação de referência.

