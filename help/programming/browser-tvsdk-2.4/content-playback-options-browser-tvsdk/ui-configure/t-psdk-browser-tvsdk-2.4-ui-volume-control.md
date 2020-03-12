---
description: Você pode configurar um controle da interface do usuário para o volume de som.
seo-description: Você pode configurar um controle da interface do usuário para o volume de som.
seo-title: Fornecer controle de volume
title: Fornecer controle de volume
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Fornecer controle de volume{#provide-volume-control}

Você pode configurar um controle da interface do usuário para o volume de som.

1. Aguarde a `MediaPlayer` instância estar em um estado válido para este comando.

   Qualquer estado, exceto RELEASED ou ERROR, é válido.
1. Defina o atributo de volume na `MediaPlayer` instância para definir o volume de áudio.

   ```js
   player.volume = ...
   ```

   O valor do volume representa o volume solicitado expresso em proporção do volume máximo, sendo 0 silencioso e o volume máximo.

