---
description: Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.
title: Reutilizar ou remover uma instância do MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Reutilizar ou remover uma instância do MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Você pode redefinir, reutilizar ou liberar uma instância do MediaPlayer que não é mais necessária.

## Redefina ou reutilize uma instância do MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando você redefine uma instância `MediaPlayer`, ela é retornada ao status IDLE não inicializado, conforme definido em `MediaPlayerStatus`.

Essa operação é útil nos seguintes casos:

* Você deseja reutilizar uma instância `MediaPlayer`, mas precisa carregar um novo `MediaResource` (conteúdo de vídeo) e substituir a instância anterior.

   A redefinição permite reutilizar a instância `MediaPlayer` sem a sobrecarga de liberar recursos, recriar o `MediaPlayer` e realocar recursos.

* Quando `MediaPlayer` estiver em status ERROR e precisar ser apagado.

   >[!IMPORTANT]
   >
   >Esta é a única maneira de recuperar do status ERROR.

   1. Chame `reset` para retornar a instância `MediaPlayer` ao status não inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Use `MediaPlayer.replaceCurrentResource()` para carregar outro `MediaResource`.

      >[!NOTE]
      >
      >Para limpar um erro, carregue o mesmo `MediaResource`.

   1. Ao receber o retorno de chamada `STATUS_CHANGED` do evento com o status `PREPARED` , inicie a reprodução.

## Liberar uma instância do MediaPlayer e recursos {#section_13A0914AFF784943ABC343F7EB249C4E}

Você deve liberar uma instância `MediaPlayer` e recursos quando não precisar mais do `MediaResource`.

Quando você lança um objeto `MediaPlayer`, os recursos de hardware subjacentes associados a esse objeto `MediaPlayer` são desalocados.

Estes são alguns motivos para lançar um `MediaPlayer`:

* A retenção de recursos desnecessários pode afetar o desempenho.
* Deixar um objeto `MediaPlayer` desnecessário instanciado pode levar ao consumo contínuo de bateria para dispositivos móveis.
* Se houver várias instâncias
Como o mesmo codec de vídeo não é compatível em um dispositivo, a falha de reprodução pode ocorrer para outros aplicativos.

* Solte o `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Depois que a instância `MediaPlayer` for lançada, não será mais possível usá-la. Se qualquer método da interface `MediaPlayer` for chamado depois de ser lançado, um `MediaPlayerException` será lançado.