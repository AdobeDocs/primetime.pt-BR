---
description: Você pode configurar um controle da interface do usuário para volume de som.
title: Fornecer controle de volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# Fornecer controle de volume{#provide-volume-control}

Você pode configurar um controle da interface do usuário para volume de som.

1. Aguarde a `MediaPlayer` instância esteja em um estado válido para este comando.

   Qualquer estado, exceto RELEASED ou ERROR, é válido.
1. Defina o atributo de volume no `MediaPlayer` instância para definir o volume de áudio.

   ```js
   player.volume = ...
   ```

   O valor do volume representa o volume solicitado expresso como uma proporção do volume máximo, onde 0 é silencioso e é o volume máximo.
