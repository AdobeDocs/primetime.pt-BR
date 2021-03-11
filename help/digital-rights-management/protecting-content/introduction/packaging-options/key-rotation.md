---
description: 'Você pode selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença '
title: Rotação da Chave
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Rotação da Chave {#key-rotation}

Você pode selecionar as seguintes opções de criptografia ao criar um pacote. No entanto, não é possível modificar as opções de criptografia durante a aquisição da licença:

Durante o empacotamento, o conteúdo normalmente é criptografado usando a Chave de criptografia de conteúdo (CEK). O cliente obtém uma licença contendo o CEK para consumir o conteúdo.

Quando você ativa a rotação de chaves, a Chave de rotação é usada para criptografar o conteúdo e a tecla pode ser alterada para que cada Chave de rotação seja usada apenas para criptografar uma parte do conteúdo. As chaves de rotação são protegidas usando a chave de criptografia de conteúdo, e o cliente ainda obtém uma licença única contendo o CEK para consumir o conteúdo.

A implementação do empacotador pode controlar a chave de criptografia de conteúdo e as chaves de rotação usadas, bem como a frequência com que as chaves de rotação são alteradas.

>[!NOTE]
>
>O conteúdo empacotado usando a rotação de chave só pode ser reproduzido em clientes DRM Primetime versão 3.0 ou posterior. Clientes mais antigos podem precisar atualizar para reproduzir esse conteúdo.