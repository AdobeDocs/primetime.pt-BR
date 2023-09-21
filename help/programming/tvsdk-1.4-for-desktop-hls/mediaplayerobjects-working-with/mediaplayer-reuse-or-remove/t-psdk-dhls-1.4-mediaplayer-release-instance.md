---
description: Você deve liberar uma instância MediaPlayer e recursos quando não precisar mais do MediaResource.
title: Liberar uma instância e recursos do MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Liberar uma instância e recursos do MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Você deve liberar uma instância MediaPlayer e recursos quando não precisar mais do MediaResource.

Quando você libera um `MediaPlayer` objeto, os recursos de hardware subjacentes associados a este `MediaPlayer` objeto são desalocados.

Aqui estão alguns motivos para lançar um `MediaPlayer`:

* Manter recursos desnecessários pode afetar o desempenho.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, pode ocorrer uma falha de reprodução para outros aplicativos.

1. Lançar o `MediaPlayer`.

   ```
   function release():void;
   ```

Depois que a variável `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método do `MediaPlayer` for chamada depois de ser lançada, uma `IllegalStateException` é lançado.
