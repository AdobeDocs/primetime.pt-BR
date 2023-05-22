---
description: Você pode redefinir, reutilizar ou liberar uma ocorrência do MediaPlayer que não é mais necessária.
title: Reutilizar ou remover uma ocorrência de MediaPlayer
exl-id: 2403e6dd-74c4-43fb-913a-d04e61041628
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Reutilizar ou remover uma ocorrência de MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma ocorrência do MediaPlayer que não é mais necessária.

## Redefinir ou reutilizar uma ocorrência de MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Você pode redefinir um `MediaPlayer` para retornar ao estado IDLE não inicializado, conforme definido na `MediaPlayerStatus`. Também é possível substituir o item de mídia atual ou definir um novo usando um recurso de mídia carregado anteriormente.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar um `MediaPlayer` instância, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substitua a instância anterior.

   A redefinição permite reutilizar o `MediaPlayer` instância sem a sobrecarga de liberação de recursos, recriando o `MediaPlayer`e realocação de recursos. A variável `replaceCurrentItem` O faz essas etapas automaticamente para você.

* Quando a variável `MediaPlayer` está em um estado ERRO e precisa ser apagado.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de se recuperar do estado ERROR.

1. Chame `MediaPlayer.reset()` para retornar a `MediaPlayer` instância ao seu estado não inicializado:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Chame `MediaPlayer.replaceCurrentItem()` para carregar outro `MediaResource`

   >[!TIP]
   >
   >Para eliminar um erro, carregue o mesmo `MediaResource`.

1. Chame o `prepareToPlay()` método.

   >[!NOTE]
   >
   >Ao receber a `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` com o estado PREPARADO, é possível iniciar a reprodução.

## Liberar uma instância e recursos do MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Você deve liberar um `MediaPlayer` e recursos quando não precisar mais do MediaResource.

Aqui estão alguns motivos para lançar um `MediaPlayer`:

* Manter recursos desnecessários pode afetar o desempenho.
* Deixar um desnecessário `MediaPlayer` pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, pode ocorrer uma falha de reprodução para outros aplicativos.

* Lançar o `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Depois que a variável `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método do `MediaPlayer` for chamada depois de ser lançada, uma `IllegalStateException` é lançado.
