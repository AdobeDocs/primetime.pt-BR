---
description: Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerStatus.
title: Redefinir ou reutilizar uma instância do MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# Redefinir ou reutilizar uma instância do MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerStatus.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar o `MediaPlayer` e realocar recursos. Os métodos `replaceCurrentItem` e `replaceCurrentResource` executam automaticamente essas etapas, sem precisar chamar o método reset .

* Quando `MediaPlayer` tiver um status ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Esta é a única maneira de recuperar do status ERROR.

1. Chame `reset` para retornar a instância `MediaPlayer` ao seu estado não inicializado:

   ```
   function reset():void; 
   ```

1. Use `MediaPlayer.replaceCurrentItem` ou `MediaPlayer.replaceCurrentResource` para carregar outro `MediaResource`.

   >[!TIP]
   >
   >Para limpar um erro, carregue o mesmo `MediaResource`.

1. Ao receber o `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` com o status `PREPARED`, inicie a reprodução.
