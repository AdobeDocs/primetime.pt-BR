---
description: O utilitário Scrambler de senha criptografa uma senha para o Adobe Primetime DRM Server para arquivos de configuração de transmissão protegida.
seo-description: O utilitário Scrambler de senha criptografa uma senha para o Adobe Primetime DRM Server para arquivos de configuração de transmissão protegida.
seo-title: Senha
title: Senha
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# Senha {#password-scrambler}

O utilitário Scrambler de senha criptografa uma senha para o Adobe Primetime DRM Server para arquivos de configuração de transmissão protegida.

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

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>O utilitário Scrambler de senha no Primetime DRM Server for Protected Streaming não é intercambiável com o arranhador fornecido com o Servidor de Licença de Implementação de Referência.