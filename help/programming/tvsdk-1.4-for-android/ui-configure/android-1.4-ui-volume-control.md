---
description: Você pode configurar um controle da interface do usuário para volume de som.
title: Fornecer controle de volume
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Fornecer controle de volume{#provide-volume-control}

Você pode configurar um controle da interface do usuário para volume de som.

1. Aguarde até que a ocorrência de MediaPlayer esteja em um estado válido para esse comando, que é qualquer um exceto RELEASED ou ERROR.
1. Chame `setVolume` no `MediaPlayer` instância para definir o volume de áudio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   O valor do volume representa o volume solicitado expresso como uma proporção do volume máximo, onde 0 é silencioso e 100 é o volume máximo.
