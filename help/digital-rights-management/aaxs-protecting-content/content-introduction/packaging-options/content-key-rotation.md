---
description: As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.
seo-description: As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.
seo-title: Rotação da tecla
title: Rotação da tecla
uuid: 6ee47c06-9981-4281-b10b-343f8b1e55b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Rotação da tecla{#key-rotation}

As opções de criptografia a seguir são selecionadas no momento do empacotamento e não podem ser modificadas durante a aquisição da licença.

Durante o empacotamento, normalmente o conteúdo é criptografado usando a Chave de criptografia de conteúdo (CEK), e o cliente obtém uma licença contendo o CEK para consumir o conteúdo. Quando a rotação de chaves está ativada, a Chave de rotação é usada para criptografar o conteúdo e a chave pode ser alterada para que cada Chave de rotação seja usada apenas para criptografar uma parte do conteúdo. As chaves de rotação são protegidas usando a chave de criptografia de conteúdo, e o cliente ainda obtém uma única licença contendo o CEK para consumir o conteúdo. A implementação do Packager pode controlar a Chave de criptografia de conteúdo e as Chaves de rotação usadas, bem como a frequência com que as Chaves de rotação são alteradas.

O conteúdo empacotado usando a rotação de chaves só pode ser reproduzido nos clientes do Adobe Access versão 3.0 e superior. Clientes mais antigos precisariam atualizar para reproduzir este conteúdo.
