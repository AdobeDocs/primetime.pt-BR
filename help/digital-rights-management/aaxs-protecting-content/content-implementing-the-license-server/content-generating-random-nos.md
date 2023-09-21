---
title: Gerando números aleatórios
description: Gerando números aleatórios
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Gerando números aleatórios{#generating-random-numbers}

Geradores de número aleatório de hardware podem ser usados em servidores Linux para garantir que seja gerada entropia suficiente. Se a máquina não puder gerar entropia suficiente, as operações de acesso ao Adobe que requerem uma fonte de aleatoriedade serão bloqueadas enquanto aguardam os dados do `/dev/random`.
