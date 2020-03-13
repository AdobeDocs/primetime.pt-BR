---
description: 'Você pode selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença '
seo-description: 'Você pode selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença '
seo-title: Rotação da tecla
title: Rotação da tecla
uuid: 6ac3b828-2cd1-42df-b9ee-4daa8e553d5e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Rotação da tecla {#key-rotation}

Você pode selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença:

Durante o empacotamento, o conteúdo normalmente é criptografado usando a Chave de criptografia de conteúdo (CEK). O cliente obtém uma licença contendo o CEK para consumir o conteúdo.

Quando você ativa a rotação de chaves, a Chave de rotação é usada para criptografar o conteúdo e a chave pode ser alterada para que cada Chave de rotação seja usada apenas para criptografar uma parte do conteúdo. As chaves de rotação são protegidas usando a chave de criptografia de conteúdo, e o cliente ainda obtém uma única licença contendo o CEK para consumir o conteúdo.

A implementação do Packager pode controlar a Chave de criptografia de conteúdo e as Chaves de rotação usadas, bem como a frequência com que as Chaves de rotação são alteradas.

>[!NOTE]
>
>O conteúdo empacotado usando a rotação de chave só pode ser reproduzido nos clientes Primetime DRM versão 3.0 ou posterior. Clientes mais antigos podem precisar atualizar para reproduzir este conteúdo.