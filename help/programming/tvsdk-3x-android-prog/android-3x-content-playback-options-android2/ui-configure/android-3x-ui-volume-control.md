---
description: Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.
title: Fornecer controle de volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 2%

---


# Fornecer controle de volume {#provide-volume-control}

Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.

1. Na rotina de retorno de chamada do elemento da interface de controle de volume, verifique se o player está em um status válido para esse comando.

   >[!TIP]
   >
   >Qualquer status, exceto LIBERADO, é válido.

1. Chame `setVolume` para definir o volume de áudio.

   Por exemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   O valor do volume representa o volume solicitado expresso em proporção do volume máximo, em que `0` é silencioso e `1` é o volume máximo.