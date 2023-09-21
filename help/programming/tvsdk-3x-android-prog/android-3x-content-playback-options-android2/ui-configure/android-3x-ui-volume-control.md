---
description: É possível configurar um controle da interface do usuário para ajustar o volume do vídeo.
title: Fornecer controle de volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Fornecer controle de volume {#provide-volume-control}

É possível configurar um controle da interface do usuário para ajustar o volume do vídeo.

1. Na rotina de retorno de chamada do elemento da interface de controle de volume, verifique se o player está em um status válido para esse comando.

   >[!TIP]
   >
   >Qualquer status, exceto LIBERADO, é válido.

1. Chame `setVolume` para definir o volume de áudio.

   Por exemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   O valor do volume representa o volume solicitado expresso em proporção do volume máximo, sendo `0` é silencioso e `1` é o volume máximo.
