---
seo-title: Criptografia de chave assimétrica
title: Criptografia de chave assimétrica
uuid: 0aae25f1-a609-4c73-9aef-13f8ae63f6e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Criptografia de chave assimétrica{#asymmetric-key-encryption}

A criptografia de chave assimétrica (também chamada de criptografia de chave pública) usa pares de chaves. É utilizada uma chave para encriptação; a outra para decodificação. A chave de decodificação é mantida em segredo e é chamada de chave ** privada. A chave de criptografia, chamada de chave ** pública, é disponibilizada para qualquer pessoa autorizada a criptografar conteúdo. Qualquer pessoa com acesso à chave pública pode criptografar o conteúdo, mas somente alguém com acesso à chave privada pode descriptografá-lo. A chave privada não pode ser reconstruída a partir da chave pública.

Ao empacotar conteúdo, a chave pública do License Server é usada para criptografar a chave de criptografia de conteúdo (CEK) nos metadados do DRM. Você deve garantir que somente o License Server tenha acesso à chave privada do License Server; se outra pessoa tiver a chave, ela poderá descriptografar e exibir o conteúdo.

***Cuidado:**Certifique-se de obter o certificado do License Server (que contém a chave pública) de uma fonte confiável para ter certeza de que é a chave do License Server e não uma chave pública desconhecida. Se um invasor substituísse a chave pública pela chave do License Server, ele seria capaz de descriptografar seu conteúdo.*

Para obter mais informações sobre como empacotar conteúdo, consulte *Uso do SDK do Adobe Access para Proteção de Conteúdo*.
