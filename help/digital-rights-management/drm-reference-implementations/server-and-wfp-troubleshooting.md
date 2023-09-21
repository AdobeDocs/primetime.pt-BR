---
title: Solução de problemas
description: Solução de problemas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Solução de problemas{#troubleshooting}

A seguir estão alguns problemas e soluções que você pode encontrar durante a implantação.

* Se a seguinte mensagem de erro for exibida:

  ```
  "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Verifique se a senha foi criptografada com o `ScrambleUtil` classe.

* Se a seguinte mensagem de erro for exibida:

  ```
  "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Verifique se você especificou a senha criptografada correta no arquivo PFX.

* Se a seguinte mensagem de erro for exibida:

  ```
  "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Certifique-se de usar a classe do codificador de senhas *que foi fornecido com a implementação de referência*. Esse utilitário scrambler é diferente do que foi fornecido com o Adobe Primetime DRM Server para transmissão protegida.
