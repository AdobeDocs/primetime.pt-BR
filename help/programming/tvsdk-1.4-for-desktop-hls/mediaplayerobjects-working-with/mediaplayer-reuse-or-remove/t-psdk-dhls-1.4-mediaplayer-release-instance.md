---
description: Você deve lançar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.
title: Liberar uma instância e recursos do MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Liberar uma instância do MediaPlayer e recursos{#release-a-mediaplayer-instance-and-resources}

Você deve lançar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.

Quando você lança um objeto `MediaPlayer`, os recursos de hardware subjacentes associados a esse objeto `MediaPlayer` são desalocados.

Estes são alguns motivos para lançar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, a falha de reprodução poderá ocorrer em outros aplicativos.

1. Solte o `MediaPlayer`.

   ```
   function release():void;
   ```

Depois que a instância `MediaPlayer` for lançada, não será mais possível usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois de ser lançado, um `IllegalStateException` será lançado.