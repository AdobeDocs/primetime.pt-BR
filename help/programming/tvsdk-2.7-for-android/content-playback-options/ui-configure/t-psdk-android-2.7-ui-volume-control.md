---
description: Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.
seo-description: Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.
seo-title: Fornecer controle de volume
title: Fornecer controle de volume
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Fornecer controle de volume {#provide-volume-control}

Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.

1. Na rotina de retorno de chamada do elemento de interface de controle de volume, verifique se o player está em um status válido para esse comando.

   >[!TIP]
   >
   >Qualquer status, exceto para LIBERADO, é válido.

1. Chame `setVolume` para definir o volume de áudio.

   Por exemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   O valor do volume corresponde ao volume solicitado expresso em percentagem do volume máximo, em que `0` é silencioso e `1` é o volume máximo.

