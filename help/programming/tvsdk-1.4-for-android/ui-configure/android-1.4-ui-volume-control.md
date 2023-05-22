---
description: Você pode configurar um controle da interface do usuário para volume de som.
title: Fornecer controle de volume
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
