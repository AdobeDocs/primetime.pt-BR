---
description: nulo
seo-description: nulo
seo-title: Solução de problemas
title: Solução de problemas
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Solução de problemas{#troubleshooting}

Veja a seguir alguns problemas e soluções que você pode encontrar durante a implantação.

* Se a seguinte mensagem de erro for exibida:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Verifique se a senha foi criptografada com a `ScrambleUtil` classe.

* Se a seguinte mensagem de erro for exibida:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Verifique se você especificou a senha criptografada correta no arquivo PFX.

* Se a seguinte mensagem de erro for exibida:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Certifique-se de usar a classe de script de senha *fornecida com a Implementação* de referência. Este utilitário de arranhador é diferente daquele fornecido com o Adobe Primetime DRM Server para Protected Streaming.

