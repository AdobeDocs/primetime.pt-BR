---
description: As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.
title: Rotação da Chave
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Rotação da Chave{#key-rotation}

As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.

Durante a embalagem, normalmente o conteúdo é criptografado usando a Chave de criptografia de conteúdo (CEK), e o cliente obtém uma licença contendo o CEK para consumir o conteúdo. Quando a rotação de chaves está ativada, a Chave de rotação é usada para criptografar o conteúdo e a tecla pode ser alterada para que cada Chave de rotação seja usada apenas para criptografar uma parte do conteúdo. As chaves de rotação são protegidas usando a chave de criptografia de conteúdo, e o cliente ainda obtém uma licença única contendo o CEK para consumir o conteúdo. A implementação do empacotador pode controlar a chave de criptografia de conteúdo e as chaves de rotação usadas, bem como a frequência com que as chaves de rotação são alteradas.

O conteúdo empacotado usando a rotação de chave só pode ser reproduzido nos clientes do Adobe Access versão 3.0 e superior. Clientes mais antigos precisariam atualizar para reproduzir esse conteúdo.
