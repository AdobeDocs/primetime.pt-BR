---
title: Glossário
description: Termos usados com frequência que exigem definição especial.
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Glossário {#glossary}

Termos usados com frequência que exigem definição especial.

## Chave de criptografia de conteúdo {#content-encryption-key}

A chave de criptografia de conteúdo (CEK), gerada por um utilitário, é usada posteriormente por um pacote de conteúdo na preparação de conteúdo que deve ser protegido.
O utilitário gera a chave em hexadecimal com um comprimento de 16 bytes.
Este guia mostra, em notas e mensagens de erro, arquivos e exemplos de comando, as seguintes variantes de nomes de parâmetros e nomes de valores para o CEK:

* chave de conteúdo
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Os nomes de arquivo para um CEK são mostrados como:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

O próprio CEK pode ser armazenado em um sistema de gerenciamento de chaves, bem como criptografado. Este guia se refere ao índice de armazenamento como CEK Storage ID CEKSID. O termo Chave de criptografia de chave (KEK) se refere à chave de criptografia de segundo nível e o termo `ek` se refere ao valor dessa criptografia.
Algumas chamadas usam o CEK e o CEK Storage ID CEKSID, e o CEK recuperado do armazenamento deve corresponder ao CEK fornecido na chamada .
Para o HLS Offline com o FairPlay, também há um `persistentContentKey` que pode ser definido para expirar.

## ID de armazenamento da chave de criptografia de conteúdo {#content-encryption-key-storage-id}

A Content Encryption Key Storage ID (CEKSID) é uma ID para recuperar uma chave de criptografia de conteúdo de um sistema de gerenciamento de chaves.

O CEKSID é também referido como
* Key ID
* ID de conteúdo
* `&kid`

## Autenticador de cliente {#customer-authenticator}

Uma chave para autenticação em solicitações à API do Express. As solicitações podem incluir solicitações de tokens.
