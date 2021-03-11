---
description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
title: Reutilizar ou remover uma instância do MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Reutilizar ou remover uma instância do MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

## Redefina ou reutilize uma instância do MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Você pode redefinir uma instância `MediaPlayer` para retorná-la ao seu estado IDLE não inicializado, conforme definido em `MediaPlayerStatus`. Você também pode substituir o item de mídia atual ou definir um novo usando um recurso de mídia carregado anteriormente.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar o `MediaPlayer` e realocar recursos. O método `replaceCurrentItem` faz automaticamente essas etapas para você.

* Quando `MediaPlayer` estiver em um estado ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de recuperar do estado ERROR.

1. Chame `MediaPlayer.reset()` para retornar a instância `MediaPlayer` ao seu estado não inicializado:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Chame `MediaPlayer.replaceCurrentItem()` para carregar outro `MediaResource`

   >[!TIP]
   >
   >Para limpar um erro, carregue o mesmo `MediaResource`.

1. Chame o método `prepareToPlay()`.

   >[!NOTE]
   >
   >Ao receber o evento `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` com o estado PREPARADO, é possível iniciar a reprodução.

## Liberar uma instância do MediaPlayer e recursos {#section_2D159975C82245098E7078FE0B1578CE}

Você deve lançar uma instância `MediaPlayer` e recursos quando não precisar mais do MediaResource.

Estes são alguns motivos para lançar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto `MediaPlayer` desnecessário pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, a falha de reprodução poderá ocorrer em outros aplicativos.

* Solte o `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Depois que a instância `MediaPlayer` for lançada, não será mais possível usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois de ser lançado, um `IllegalStateException` será lançado.

