---
description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-title: Reutilizar ou remover uma instância MediaPlayer
title: Reutilizar ou remover uma instância MediaPlayer
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Reutilize ou remova uma instância do MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

## Redefina ou reutilize uma instância do MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Você pode redefinir uma instância `MediaPlayer` para retorná-la ao seu estado IDLE não inicializado, conforme definido em `MediaPlayerStatus`. Você também pode substituir o item de mídia atual ou definir um novo usando um recurso de mídia carregado anteriormente.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar uma nova `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar `MediaPlayer` e realocar recursos. O método `replaceCurrentItem` faz automaticamente essas etapas para você.

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
   >Para apagar um erro, carregue o mesmo `MediaResource`.

1. Chame o método `prepareToPlay()`.

   >[!NOTE]
   >
   >Ao receber o evento `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` com o estado PREPARADO, você pode start a reprodução.

## Liberar uma instância e recursos do MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Você deve liberar uma instância `MediaPlayer` e recursos quando não precisar mais do MediaResource.

Estes são alguns motivos para liberar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto `MediaPlayer` desnecessário pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, poderá ocorrer uma falha na reprodução em outros aplicativos.

* Solte o `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Depois que a instância `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois que for lançado, um `IllegalStateException` será lançado.

