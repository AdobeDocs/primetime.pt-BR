---
title: Criptografia de chave assimétrica
description: Criptografia de chave assimétrica
copied-description: true
exl-id: 5962176e-07ec-4606-b1d8-39946ba59127
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Criptografia de chave assimétrica{#asymmetric-key-encryption}

A criptografia de chave assimétrica (também chamada de criptografia de chave pública) usa pares de chaves. Uma chave é usada para criptografia; a outra para descriptografia. A chave de descriptografia é mantida em segredo e é chamada de *chave privada*. A chave de criptografia, chamada de *chave pública*, é disponibilizado a qualquer pessoa autorizada a criptografar conteúdo. Qualquer pessoa com acesso à chave pública pode criptografar o conteúdo, mas somente alguém com acesso à chave privada pode descriptografar o conteúdo. A chave privada não pode ser reconstruída a partir da chave pública.

Ao empacotar conteúdo, a chave pública do License Server será usada para criptografar a chave de criptografia de conteúdo (CEK) nos metadados de DRM. Você deve garantir que somente o License Server tenha acesso à chave privada do License Server. Se outra pessoa tiver a chave, ela poderá descriptografar e exibir o conteúdo.

***Atenção:**Certifique-se de obter o certificado do License Server (contendo a chave pública) de uma fonte confiável, para poder ter certeza de que é a chave do License Server e não uma chave pública não autorizada. Se um invasor substituir a chave pública pela chave do License Server, poderá descriptografar o conteúdo.*

Para obter mais informações sobre o conteúdo da embalagem, consulte *Utilização do SDK do Adobe Access para proteção de conteúdo*.
