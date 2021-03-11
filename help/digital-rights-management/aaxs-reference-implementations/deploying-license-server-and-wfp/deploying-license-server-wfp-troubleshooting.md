---
title: Solução de problemas
description: Solução de problemas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Solução de problemas {#troubleshooting}

Veja abaixo os problemas e soluções comuns para implantação:

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

   Certifique-se de especificar a senha criptografada correta para o arquivo PFX.

* Se você vir o seguinte erro:

   ```
       "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Certifique-se de usar a classe de arranhador de senha fornecida com a Implementação de referência (este utilitário é diferente daquele fornecido com o Adobe® Access™ Server for Protected Streaming).

