---
title: Gerando números aleatórios
description: Gerando números aleatórios
copied-description: true
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Gerando números aleatórios{#generating-random-numbers}

Geradores de número aleatório de hardware podem ser usados em servidores Linux para garantir que seja gerada entropia suficiente. Se a máquina não puder gerar entropia suficiente, as operações de acesso ao Adobe que requerem uma fonte de aleatoriedade serão bloqueadas enquanto aguardam os dados do `/dev/random`.
