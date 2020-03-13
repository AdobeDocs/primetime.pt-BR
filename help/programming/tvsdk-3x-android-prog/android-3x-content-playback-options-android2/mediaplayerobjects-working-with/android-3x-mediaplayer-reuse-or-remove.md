---
description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-title: Reutilizar ou remover uma instância MediaPlayer
title: Reutilizar ou remover uma instância MediaPlayer
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Reutilizar ou remover uma instância MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

## Redefinir ou reutilizar uma instância MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando você redefine uma `MediaPlayer` instância, ela é retornada ao seu status IDLE não inicializado, conforme definido em `MediaPlayerStatus`.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma `MediaPlayer` instância, mas precisa carregar uma nova `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a `MediaPlayer` instância sem a sobrecarga de liberar recursos, recriar os recursos `MediaPlayer`e realocar os recursos.

* Quando o estado `MediaPlayer` estiver em ERROR e precisar de ser limpo.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de recuperar do status ERROR.

   1. Chame `reset` para retornar a `MediaPlayer` instância ao seu status não inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Use `MediaPlayer.replaceCurrentResource()` para carregar outro `MediaResource`.

      >[!NOTE]
      >
      >Para apagar um erro, carregue o mesmo `MediaResource`.

   1. Ao receber o retorno de chamada do `STATUS_CHANGED` evento com `PREPARED` status, inicie a reprodução.

## Liberar uma instância e recursos do MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Você deve liberar uma `MediaPlayer` instância e recursos quando não precisar mais do `MediaResource`.

Quando você solta um `MediaPlayer` objeto, os recursos de hardware subjacentes associados a esse `MediaPlayer` objeto são desalocados.

Estes são alguns motivos para lançar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto desnecessário instanciado pode levar ao consumo contínuo de bateria para dispositivos móveis. `MediaPlayer`
* Se várias instâncias do mesmo codec de vídeo não forem suportadas em um dispositivo, poderá ocorrer uma falha na reprodução em outros aplicativos.

* Solte o `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Depois que a `MediaPlayer` instância é liberada, não é mais possível usá-la. Se qualquer método da `MediaPlayer` interface for chamado após sua liberação, um `MediaPlayerException` será lançado.