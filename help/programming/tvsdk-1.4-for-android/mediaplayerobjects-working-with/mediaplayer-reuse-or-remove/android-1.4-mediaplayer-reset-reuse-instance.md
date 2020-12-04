---
description: Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerState.
seo-description: Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerState.
seo-title: Redefinir ou reutilizar uma instância MediaPlayer
title: Redefinir ou reutilizar uma instância MediaPlayer
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Redefinir, reutilizar ou remover uma instância MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerState.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar uma nova `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar `MediaPlayer` e realocar recursos.

* Quando `MediaPlayer` estiver em um estado ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de recuperar do estado ERROR.

1. Chame `reset` para retornar a instância `MediaPlayer` ao seu estado não inicializado:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Use `MediaPlayer.replaceCurrentResource` para carregar outro `MediaResource`.

   >[!TIP]
   >
   >Para apagar um erro, carregue o mesmo `MediaResource`.

1. Ao receber o retorno de chamada do evento `STATUS_CHANGED` com o status PREPARADO, start a reprodução.

## Liberar uma instância e recursos do MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Você deve liberar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.

Quando você solta um objeto `MediaPlayer`, os recursos de hardware subjacentes associados a esse objeto `MediaPlayer` são desalocados.

Estes são alguns motivos para liberar um MediaPlayer:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto `MediaPlayer` desnecessário pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, poderá ocorrer uma falha na reprodução em outros aplicativos.

1. Solte o `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Depois que a instância `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois que for lançado, um `IllegalStateException` será lançado.