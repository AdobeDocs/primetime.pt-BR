---
title: Solução de problemas
description: Solução de problemas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Solução de problemas {#troubleshooting}

Os problemas comuns e as soluções para implantação estão listados abaixo:

* Se você vir o seguinte erro:

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Verifique se a senha está criptografada usando o `ScrambleUtil` classe.

* Se você vir o seguinte erro:

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Verifique se você especificou a senha criptografada correta para o arquivo PFX.

* Se você vir o seguinte erro:

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Certifique-se de ter usado a classe de scrambler de senha fornecida com a Implementação de referência (este utilitário de scrambler é diferente do fornecido com o servidor Adobe® Access™ para transmissão protegida).
