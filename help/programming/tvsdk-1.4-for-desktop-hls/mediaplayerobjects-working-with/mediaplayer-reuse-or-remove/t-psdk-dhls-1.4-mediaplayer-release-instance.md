---
description: Você deve liberar uma instância MediaPlayer e recursos quando não precisar mais do MediaResource.
title: Liberar uma instância e recursos do MediaPlayer
exl-id: 2a802754-5c51-4e5f-8c36-843074b487b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
