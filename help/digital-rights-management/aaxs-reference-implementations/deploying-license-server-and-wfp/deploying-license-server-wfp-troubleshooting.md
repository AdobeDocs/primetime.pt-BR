---
seo-title: Solução de problemas
title: Solução de problemas
uuid: db76d6a4-c285-4d86-95a1-4f1a85ed3743
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Solução de problemas {#troubleshooting}

A seguir estão listados problemas comuns e soluções para implantação:

* Se você vir o seguinte erro:

   ```
       "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Verifique se a senha está criptografada usando a classe `ScrambleUtil` fornecida.

* Se você vir o seguinte erro:

   ```
       "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Verifique se você especificou a senha criptografada correta para o arquivo PFX.

* Se você vir o seguinte erro:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Certifique-se de usar a classe do arranhador de senha fornecida com a Implementação de referência (este utilitário é diferente daquele fornecido com o Adobe® Access™ Server para Protected Streaming).

