---
description: Quando você redefine uma instância do MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerStatus.
seo-description: Quando você redefine uma instância do MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerStatus.
seo-title: Redefinir ou reutilizar uma instância MediaPlayer
title: Redefinir ou reutilizar uma instância MediaPlayer
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Redefinir ou reutilizar uma instância MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

Quando você redefine uma instância do MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerStatus.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar uma nova `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar `MediaPlayer` e realocar recursos. Os métodos `replaceCurrentItem` e `replaceCurrentResource` fazem automaticamente essas etapas para você, sem precisar chamar o método reset.

* Quando `MediaPlayer` tiver um status ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de recuperar do status ERROR.

1. Chame `reset` para retornar a instância `MediaPlayer` ao seu estado não inicializado:

   ```
   function reset():void; 
   ```

1. Use `MediaPlayer.replaceCurrentItem` ou `MediaPlayer.replaceCurrentResource` para carregar outro `MediaResource`.

   >[!TIP]
   >
   >Para apagar um erro, carregue o mesmo `MediaResource`.

1. Quando você receber o `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` com o status `PREPARED`, start a reprodução.
