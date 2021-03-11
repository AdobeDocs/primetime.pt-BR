---
title: Geração de números aleatórios
description: Geração de números aleatórios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# Gerando números aleatórios{#generating-random-numbers}

Geradores de números aleatórios de hardware podem ser usados em servidores Linux para garantir que seja gerada entropia suficiente. Se a máquina não puder gerar entropia suficiente, as operações de Adobe Access que exigem uma fonte de aleatoriedade serão bloqueadas enquanto aguardam os dados de `/dev/random`.
