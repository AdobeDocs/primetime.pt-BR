---
description: Você pode configurar um controle da interface do usuário para volume de som.
title: Fornecer controle de volume
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
