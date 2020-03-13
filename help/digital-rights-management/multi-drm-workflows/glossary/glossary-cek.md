---
uuid: 2d927ae8-4c4b-4b64-88b8-9c86430e226c
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Glossário {#glossary}

Termos usados com frequência que exigem uma definição especial.

## Chave de criptografia de conteúdo {#content-encryption-key}

A chave de criptografia de conteúdo (CEK), gerada por um utilitário, é usada subsequentemente por um empacotador de conteúdo na preparação de conteúdo que deve ser protegido.
O utilitário gera a chave em hexadecimal com um comprimento de 16 bytes.
Este guia mostra, em notas e mensagens de erro, arquivos e amostras de comando, as seguintes variantes de nomes de parâmetros e nomes de valores para o CEK:

* chave de conteúdo
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Os nomes de arquivo para um CEK são mostrados como:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

O próprio CEK pode ser armazenado em um sistema de gerenciamento de chaves, bem como criptografado. Este guia se refere ao índice de armazenamento como CEK Storage ID CEKSID. O termo Chave de criptografia (KEK) refere-se à chave de criptografia de segundo nível e o termo `ek` refere-se ao valor dessa criptografia.
Algumas chamadas usam o CEK e o CEK Storage ID CEKSID, e o CEK recuperado do armazenamento deve corresponder ao CEK fornecido na chamada.
Para HLS offline com FairPlay, também há um `persistentContentKey` que pode ser definido para expirar.

## ID de armazenamento da chave de criptografia de conteúdo {#content-encryption-key-storage-id}

A ID de armazenamento da chave de criptografia de conteúdo (CEKSID) é uma ID para recuperar uma chave de criptografia de conteúdo de um sistema de gerenciamento de chaves.

O CEKSID é também referido como
* ID da chave
* ID do conteúdo
* `&kid`

## Autenticador do cliente {#customer-authenticator}

Uma chave para autenticação em solicitações à API do Express. As solicitações podem incluir solicitações de tokens.