---
description: Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.
seo-description: Você pode configurar um controle da interface do usuário para ajustar o volume do vídeo.
seo-title: Fornecer controle de volume
title: Fornecer controle de volume
uuid: c87fe656-0329-4c9c-b65b-43be48c77062
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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