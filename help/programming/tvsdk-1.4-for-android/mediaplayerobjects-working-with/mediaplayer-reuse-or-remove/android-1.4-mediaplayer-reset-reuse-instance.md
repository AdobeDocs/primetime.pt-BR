---
description: Ao redefinir uma ocorrência de MediaPlayer, ela retorna ao estado IDLE não inicializado, conforme definido em MediaPlayerState.
title: Redefinir ou reutilizar uma ocorrência de MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Redefinir, reutilizar ou remover uma ocorrência de MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma ocorrência do MediaPlayer que não é mais necessária.

Ao redefinir uma ocorrência de MediaPlayer, ela retorna ao estado IDLE não inicializado, conforme definido em MediaPlayerState.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar um `MediaPlayer` instância, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substitua a instância anterior.

  A redefinição permite reutilizar o `MediaPlayer` instância sem a sobrecarga de liberação de recursos, recriando o `MediaPlayer`e realocação de recursos.

* Quando a variável `MediaPlayer` está em um estado ERRO e precisa ser apagado.

  >[!IMPORTANT]
  >
  >Essa é a única maneira de se recuperar do estado ERROR.

1. Chame `reset` para retornar a `MediaPlayer` instância ao seu estado não inicializado:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Uso `MediaPlayer.replaceCurrentResource` para carregar outro `MediaResource`.

   >[!TIP]
   >
   >Para eliminar um erro, carregue o mesmo `MediaResource`.

1. Ao receber a `STATUS_CHANGED` retorno de chamada de evento com status PREPARADO, inicie a reprodução.

## Liberar uma instância e recursos do MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Você deve liberar uma instância MediaPlayer e recursos quando não precisar mais do MediaResource.

Quando você libera um `MediaPlayer` objeto, os recursos de hardware subjacentes associados a este `MediaPlayer` objeto são desalocados.

Aqui estão alguns motivos para lançar um MediaPlayer:

* Manter recursos desnecessários pode afetar o desempenho.
* Deixar um desnecessário `MediaPlayer` pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, pode ocorrer uma falha de reprodução para outros aplicativos.

1. Lançar o `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Depois que a variável `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método do `MediaPlayer` for chamada depois de ser lançada, uma `IllegalStateException` é lançado.
