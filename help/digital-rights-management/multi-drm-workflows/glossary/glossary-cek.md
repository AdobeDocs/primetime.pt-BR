---
title: Glossário
description: Termos usados com frequência que exigem definição especial.
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Glossário {#glossary}

Termos usados com frequência que exigem definição especial.

## Chave de criptografia do conteúdo {#content-encryption-key}

A Chave de criptografia de conteúdo (CEK), gerada por um utilitário, é usada subsequentemente por um empacotador de conteúdo na preparação do conteúdo que deve ser protegido.
O utilitário gera a chave em hexadecimal com um comprimento de 16 bytes.
Este guia mostra, em amostras de notas e mensagens de erro, arquivos e comandos, as seguintes variantes de nomes de parâmetros e nomes de valores para o CEK:

* chave de conteúdo
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Os nomes de arquivo de um CEK são mostrados como:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

O CEK em si pode ser armazenado em um sistema de gerenciamento de chaves, bem como criptografado. Este guia se refere ao índice de armazenamento como a ID de armazenamento do CEK CEKSID. O termo Chave de criptografia (KEK) refere-se à chave de criptografia de segundo nível e ao termo `ek` refere-se ao valor dessa criptografia.
Algumas chamadas usam o CEK e o CEK Storage ID CEKSID, e o CEK recuperado do armazenamento deve corresponder ao CEK fornecido na chamada.
Para HLS Offline com FairPlay, também há uma `persistentContentKey` que pode ser definido para expirar.

## ID de armazenamento da chave de criptografia do conteúdo {#content-encryption-key-storage-id}

A ID de armazenamento da chave de criptografia de conteúdo (CEKSID) é uma ID para recuperar uma chave de criptografia de conteúdo de um sistema de gerenciamento de chaves.

O CEKSID é também referido como
* ID da chave
* ID de conteúdo
* `&kid`

## Autenticador do cliente {#customer-authenticator}

Uma chave para autenticação em solicitações para a API do Expressplay. As solicitações podem incluir solicitações de tokens.
