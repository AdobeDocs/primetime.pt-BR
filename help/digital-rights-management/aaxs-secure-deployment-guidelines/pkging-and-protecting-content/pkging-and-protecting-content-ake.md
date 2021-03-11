---
title: Criptografia de chave assimétrica
description: Criptografia de chave assimétrica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Criptografia de chave assimétrica{#asymmetric-key-encryption}

A criptografia de chave assimétrica (também chamada de criptografia de chave pública) usa pares de chaves. É utilizada uma chave para encriptação; o outro para descriptografia. A chave de descriptografia é mantida secreta e é chamada de *chave privada*. A chave de criptografia, chamada de *chave pública*, é disponibilizada para qualquer pessoa autorizada a criptografar conteúdo. Qualquer pessoa com acesso à chave pública pode criptografar o conteúdo, mas somente alguém com acesso à chave privada pode descriptografar o conteúdo. A chave privada não pode ser reconstruída a partir da chave pública.

Ao empacotar conteúdo, a chave pública do License Server é usada para criptografar a chave de criptografia de conteúdo (CEK) nos metadados DRM. Você deve garantir que somente o License Server tenha acesso à chave privada do License Server; se outra pessoa tiver a chave, ela poderá descriptografar e exibir o conteúdo.

***Cuidado:**certifique-se de obter o certificado do License Server (contendo a chave pública) de uma fonte confiável para ter certeza de que é a chave do License Server, e não uma chave pública não autorizada. Se um invasor substituísse sua chave pública pela chave do License Server, ele seria capaz de descriptografar seu conteúdo.*

Para obter mais informações sobre como empacotar conteúdo, consulte *Usar o SDK de acesso ao Adobe para proteger conteúdo*.
