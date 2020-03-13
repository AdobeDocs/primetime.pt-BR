---
description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-title: Reutilizar ou remover uma instância MediaPlayer
title: Reutilizar ou remover uma instância MediaPlayer
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Reutilizar ou remover uma instância MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

## Redefinir ou reutilizar uma instância MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

É possível redefinir uma `MediaPlayer` instância para retorná-la ao seu estado IDLE não inicializado, conforme definido em `MediaPlayerStatus`. Você também pode substituir o item de mídia atual ou definir um novo usando um recurso de mídia carregado anteriormente.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma `MediaPlayer` instância, mas precisa carregar uma nova `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a `MediaPlayer` instância sem a sobrecarga de liberar recursos, recriar os recursos `MediaPlayer`e realocar os recursos. O `replaceCurrentItem` método faz automaticamente essas etapas para você.

* Quando o `MediaPlayer` estiver em um estado ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de recuperar do estado ERROR.

1. Chame `MediaPlayer.reset()` para retornar a `MediaPlayer` instância ao seu estado não inicializado:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Chamar `MediaPlayer.replaceCurrentItem()` para carregar outro `MediaResource`

   >[!TIP]
   >
   >Para apagar um erro, carregue o mesmo `MediaResource`.

1. Chame o `prepareToPlay()` método.

   >[!NOTE]
   >
   >Ao receber o `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` evento com o estado PREPARADO, você pode iniciar a reprodução.

## Liberar uma instância e recursos do MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Você deve liberar uma `MediaPlayer` instância e recursos quando não precisar mais do MediaResource.

Estes são alguns motivos para lançar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto desnecessário pode levar ao consumo contínuo de bateria para dispositivos móveis. `MediaPlayer`
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, poderá ocorrer uma falha na reprodução em outros aplicativos.

* Solte o `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Depois que a `MediaPlayer` instância é liberada, não é mais possível usá-la. Se qualquer método da `MediaPlayer` interface for chamado após sua liberação, um `IllegalStateException` é lançado.

