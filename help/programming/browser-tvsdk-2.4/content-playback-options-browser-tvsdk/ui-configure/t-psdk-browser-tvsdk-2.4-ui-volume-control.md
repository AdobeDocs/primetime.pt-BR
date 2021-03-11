---
description: Você pode configurar um controle da interface do usuário para o volume de som.
title: Fornecer controle de volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---


# Fornecer controle de volume{#provide-volume-control}

Você pode configurar um controle da interface do usuário para o volume de som.

1. Aguarde até que a instância `MediaPlayer` esteja em um estado válido para esse comando.

   Qualquer estado, exceto LIBERADO ou ERRO, é válido.
1. Defina o atributo de volume na instância `MediaPlayer` para definir o volume de áudio.

   ```js
   player.volume = ...
   ```

   O valor do volume representa o volume solicitado expresso em proporção do volume máximo, em que 0 é silencioso e corresponde ao volume máximo.

