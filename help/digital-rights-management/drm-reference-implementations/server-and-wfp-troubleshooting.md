---
title: Solução de problemas
description: Solução de problemas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

   Verifique se a senha foi criptografada com a classe `ScrambleUtil`.

* Se a seguinte mensagem de erro for exibida:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Certifique-se de ter especificado a senha criptografada correta no arquivo PFX.

* Se a seguinte mensagem de erro for exibida:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Certifique-se de usar a classe do arranhador de senha *que foi fornecida com a Implementação de Referência*. Este utilitário de software de rabisco é diferente daquele que foi fornecido com o Adobe Primetime DRM Server for Protected Streaming.

