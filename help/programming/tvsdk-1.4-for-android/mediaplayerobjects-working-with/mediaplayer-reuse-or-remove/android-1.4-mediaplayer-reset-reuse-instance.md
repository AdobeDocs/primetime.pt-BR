---
description: Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerState.
title: Redefinir ou reutilizar uma instância do MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# Redefina, reutilize ou remova uma instância do MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

Quando você redefine uma instância MediaPlayer, ela é retornada ao seu estado IDLE não inicializado, conforme definido em MediaPlayerState.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar o `MediaPlayer` e realocar recursos.

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
   >Para limpar um erro, carregue o mesmo `MediaResource`.

1. Ao receber o retorno de chamada `STATUS_CHANGED` do evento com o status PREPARED , inicie a reprodução.

## Liberar uma instância do MediaPlayer e recursos{#release-a-mediaplayer-instance-and-resources}

Você deve lançar uma instância e recursos do MediaPlayer quando não precisar mais do MediaResource.

Quando você lança um objeto `MediaPlayer`, os recursos de hardware subjacentes associados a esse objeto `MediaPlayer` são desalocados.

Estes são alguns motivos para lançar um MediaPlayer:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto `MediaPlayer` desnecessário pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, a falha de reprodução poderá ocorrer em outros aplicativos.

1. Solte o `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Depois que a instância `MediaPlayer` for lançada, não será mais possível usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois de ser lançado, um `IllegalStateException` será lançado.