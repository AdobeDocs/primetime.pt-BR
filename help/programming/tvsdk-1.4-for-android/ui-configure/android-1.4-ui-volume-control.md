---
description: Você pode configurar um controle da interface do usuário para o volume de som.
seo-description: Você pode configurar um controle da interface do usuário para o volume de som.
seo-title: Fornecer controle de volume
title: Fornecer controle de volume
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fornecer controle de volume{#provide-volume-control}

Você pode configurar um controle da interface do usuário para o volume de som.

1. Aguarde a instância do MediaPlayer estar em um estado válido para esse comando, que é qualquer um, exceto RELEASED ou ERROR.
1. Chame `setVolume` `MediaPlayer` a instância para definir o volume de áudio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   O valor do volume representa o volume solicitado expresso em proporção do volume máximo, sendo 0 silencioso e 100 o volume máximo.

