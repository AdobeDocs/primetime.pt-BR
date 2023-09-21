---
description: É possível selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença
title: Rotação de chaves
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Rotação de chaves {#key-rotation}

É possível selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença:

Durante o empacotamento, o conteúdo normalmente é criptografado usando a Chave de criptografia do conteúdo (CEK). O cliente obtém uma licença contendo o CEK para consumir o conteúdo.

Ao ativar a rotação de chaves, a chave de rotação é usada para criptografar o conteúdo e pode ser alterada para que cada chave de rotação seja usada apenas para criptografar uma parte do conteúdo. As Chaves de rotação são protegidas usando a Chave de criptografia de conteúdo, e o cliente ainda obtém uma única licença contendo o CEK para consumir o conteúdo.

A implementação do empacotador pode controlar a Chave de criptografia do conteúdo e as Chaves de rotação usadas, bem como a frequência com que as Chaves de rotação são alteradas.

>[!NOTE]
>
>O conteúdo empacotado usando a rotação de chaves só pode ser reproduzido nos clientes DRM do Primetime versão 3.0 ou posterior. Os clientes mais antigos podem precisar atualizar para reproduzir este conteúdo.
