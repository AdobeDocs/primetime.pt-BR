---
description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
seo-title: Reutilizar ou remover uma instância MediaPlayer
title: Reutilizar ou remover uma instância MediaPlayer
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Reutilize ou remova uma instância do MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

## Redefina ou reutilize uma instância do MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando você redefine uma instância `MediaPlayer`, ela é retornada ao seu status IDLE não inicializado, conforme definido em `MediaPlayerStatus`.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar uma nova `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar `MediaPlayer` e realocar recursos.

* Quando `MediaPlayer` estiver no status ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Essa é a única maneira de recuperar do status ERROR.

   1. Chame `reset` para retornar a instância `MediaPlayer` ao seu status não inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Use `MediaPlayer.replaceCurrentResource()` para carregar outro `MediaResource`.

      >[!NOTE]
      >
      >Para apagar um erro, carregue o mesmo `MediaResource`.

   1. Quando você receber o retorno de chamada `STATUS_CHANGED` do evento com o status `PREPARED`, start a reprodução.

## Liberar uma instância e recursos do MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Você deve liberar uma instância `MediaPlayer` e recursos quando não precisar mais do `MediaResource`.

Quando você solta um objeto `MediaPlayer`, os recursos de hardware subjacentes associados a esse objeto `MediaPlayer` são desalocados.

Estes são alguns motivos para liberar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto `MediaPlayer` desnecessário instanciado pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se houver várias instâncias
s do mesmo codec de vídeo não são suportados em um dispositivo, pode ocorrer falha na reprodução em outros aplicativos.

* Solte o `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Depois que a instância `MediaPlayer` for lançada, você não poderá mais usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois que for lançado, um `MediaPlayerException` será lançado.