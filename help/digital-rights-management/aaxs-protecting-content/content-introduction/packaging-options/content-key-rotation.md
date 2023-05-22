---
description: As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.
title: Rotação de chaves
exl-id: bcb90f0e-5c61-4c56-a030-2831d9a2a962
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Rotação de chaves{#key-rotation}

As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.

Durante o empacotamento, normalmente o conteúdo é criptografado usando a Chave de criptografia de conteúdo (CEK), e o cliente obtém uma licença contendo a CEK para consumir o conteúdo. Quando a rotação de chaves está ativada, a chave de rotação é usada para criptografar o conteúdo e ela pode ser alterada para que cada chave de rotação seja usada apenas para criptografar uma parte do conteúdo. As Chaves de rotação são protegidas usando a Chave de criptografia de conteúdo, e o cliente ainda obtém uma única licença contendo o CEK para consumir o conteúdo. A implementação do empacotador pode controlar a Chave de criptografia do conteúdo e as Chaves de rotação usadas, bem como a frequência com que as Chaves de rotação são alteradas.

O conteúdo empacotado com rotação de chaves só pode ser reproduzido em clientes Adobe Access versões 3.0 e posteriores. Os clientes mais antigos precisariam atualizar para reproduzir esse conteúdo.
