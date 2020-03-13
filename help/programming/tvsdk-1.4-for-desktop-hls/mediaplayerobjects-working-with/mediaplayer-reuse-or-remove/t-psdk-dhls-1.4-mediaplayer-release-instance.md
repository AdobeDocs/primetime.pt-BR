---
description: Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.
seo-description: Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.
seo-title: Liberar uma instância e recursos do MediaPlayer
title: Liberar uma instância e recursos do MediaPlayer
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Liberar uma instância e recursos do MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.

Quando você solta um `MediaPlayer` objeto, os recursos de hardware subjacentes associados a esse `MediaPlayer` objeto são desalocados.

Estes são alguns motivos para lançar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, poderá ocorrer uma falha na reprodução em outros aplicativos.

1. Solte o `MediaPlayer`.

   ```
   function release():void;
   ```

Depois que a `MediaPlayer` instância é liberada, não é mais possível usá-la. Se qualquer método da `MediaPlayer` interface for chamado após sua liberação, um `IllegalStateException` é lançado.