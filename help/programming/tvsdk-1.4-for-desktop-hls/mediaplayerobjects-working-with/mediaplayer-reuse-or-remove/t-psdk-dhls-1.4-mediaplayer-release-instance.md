---
description: Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.
seo-description: Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.
seo-title: Liberar uma instância e recursos do MediaPlayer
title: Liberar uma instância e recursos do MediaPlayer
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Liberar uma instância e recursos do MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.

Quando você solta um objeto `MediaPlayer`, os recursos de hardware subjacentes associados a esse objeto `MediaPlayer` são desalocados.

Estes são alguns motivos para liberar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, poderá ocorrer uma falha na reprodução em outros aplicativos.

1. Solte o `MediaPlayer`.

   ```
   function release():void;
   ```

Depois que a instância `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois que for lançado, um `IllegalStateException` será lançado.