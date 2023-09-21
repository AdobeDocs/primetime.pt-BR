---
description: Você pode redefinir, reutilizar ou liberar uma ocorrência do MediaPlayer que não é mais necessária.
title: Reutilizar ou remover uma ocorrência de MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Reutilizar ou remover uma ocorrência de MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma ocorrência do MediaPlayer que não é mais necessária.

## Redefinir ou reutilizar uma ocorrência de MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Ao redefinir um `MediaPlayer` instância, ele retornará ao seu status OCIOSO não inicializado, conforme definido na `MediaPlayerStatus`

* Você deseja reutilizar um `MediaPlayer` instância, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substitua a instância anterior.

  A redefinição permite reutilizar o `MediaPlayer` instância sem a sobrecarga de liberação de recursos, recriando o `MediaPlayer`e realocação de recursos.

* Quando a variável `MediaPlayer` está no status ERRO e precisa ser apagado.

  >[!IMPORTANT]
  >
  >Essa é a única maneira de se recuperar do status ERRO.

   1. Chame `reset` para retornar a `MediaPlayer` ao seu status não inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Uso `MediaPlayer.replaceCurrentResource()` para carregar outro `MediaResource`.

      >[!NOTE]
      >
      >Para eliminar um erro, carregue o mesmo `MediaResource`.

   1. Ao receber a `STATUS_CHANGED` retorno de chamada de evento com `PREPARED` status, iniciar a reprodução.

## Liberar uma instância e recursos do MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Você deve liberar um `MediaPlayer` instância e recursos quando não precisar mais da `MediaResource`.

Quando você libera um `MediaPlayer` objeto, os recursos de hardware subjacentes associados a este `MediaPlayer` objeto são desalocados.

Aqui estão alguns motivos para lançar um `MediaPlayer`:

* Manter recursos desnecessários pode afetar o desempenho.
* Deixar um desnecessário `MediaPlayer` objeto instanciado pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, pode ocorrer uma falha de reprodução para outros aplicativos.

* Lançar o `MediaPlayer`.

  ```java
  void release() throws MediaPlayerException;
  ```

  >[!NOTE]
  >
  >Depois que a variável `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método do `MediaPlayer` for chamada depois de ser lançada, uma `MediaPlayerException` é lançado.
