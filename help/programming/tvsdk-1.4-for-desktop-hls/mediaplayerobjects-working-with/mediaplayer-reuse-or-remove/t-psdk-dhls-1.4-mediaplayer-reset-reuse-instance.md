---
description: Ao redefinir uma ocorrência de MediaPlayer, ela retorna ao estado IDLE não inicializado, conforme definido em MediaPlayerStatus.
title: Redefinir ou reutilizar uma ocorrência de MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Redefinir ou reutilizar uma ocorrência de MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma ocorrência do MediaPlayer que não é mais necessária.

Ao redefinir uma ocorrência de MediaPlayer, ela retorna ao estado IDLE não inicializado, conforme definido em MediaPlayerStatus.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar um `MediaPlayer` instância, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substitua a instância anterior.

  A redefinição permite reutilizar o `MediaPlayer` instância sem a sobrecarga de liberação de recursos, recriando o `MediaPlayer`e realocação de recursos. A variável `replaceCurrentItem` e `replaceCurrentResource` Os métodos do fazem automaticamente essas etapas para você, sem precisar chamar o método reset.

* Quando a variável `MediaPlayer` tem um status ERRO e precisa ser apagado.

  >[!IMPORTANT]
  >
  >Essa é a única maneira de se recuperar do status ERRO.

1. Chame `reset` para retornar a `MediaPlayer` instância ao seu estado não inicializado:

   ```
   function reset():void; 
   ```

1. Uso `MediaPlayer.replaceCurrentItem` ou `MediaPlayer.replaceCurrentResource` para carregar outro `MediaResource`.

   >[!TIP]
   >
   >Para eliminar um erro, carregue o mesmo `MediaResource`.

1. Quando você receber a mensagem de erro `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` com o `PREPARED` status, iniciar a reprodução.
