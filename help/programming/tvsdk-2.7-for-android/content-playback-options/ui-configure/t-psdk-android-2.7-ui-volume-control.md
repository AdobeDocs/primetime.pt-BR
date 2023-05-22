---
description: É possível configurar um controle da interface do usuário para ajustar o volume do vídeo.
title: Fornecer controle de volume
exl-id: 0daa87e2-51aa-4459-9a67-135dc54d09c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
