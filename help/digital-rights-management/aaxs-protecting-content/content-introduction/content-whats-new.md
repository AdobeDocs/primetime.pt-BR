---
description: 'O Adobe® Access™ é uma solução avançada de gerenciamento de direitos digitais e proteção de conteúdo para conteúdo audiovisual de alto valor. Usando ferramentas que você cria usando APIs Java, é possível criar políticas, aplicar políticas a arquivos que contêm conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes '
seo-description: 'O Adobe® Access™ é uma solução avançada de gerenciamento de direitos digitais e proteção de conteúdo para conteúdo audiovisual de alto valor. Usando ferramentas que você cria usando APIs Java, é possível criar políticas, aplicar políticas a arquivos que contêm conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes '
seo-title: Visão geral
title: Visão geral
uuid: 874c175b-8207-49fa-aad4-204ccbee9c2c
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Visão geral {#overview}

O Adobe® Access™ é uma solução avançada de gerenciamento de direitos digitais e proteção de conteúdo para conteúdo audiovisual de alto valor. Usando ferramentas que você cria usando APIs Java, é possível criar políticas, aplicar políticas a arquivos que contêm conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes:

1. Use as APIs Java para definir as propriedades da política e os parâmetros de criptografia.
1. Crie uma política que descreva as funções de uso do conteúdo. (Consulte [Trabalhar com políticas](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   É possível criar qualquer número de políticas. A maioria dos usuários cria um pequeno número de políticas e as aplica a muitos arquivos.

1. Empacote um arquivo de mídia.

   Neste contexto, *empacotar um arquivo* significa criptografá-lo e aplicar uma política a ele. (Consulte [Empacotamento de arquivos](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md)de mídia.)

1. Implemente o servidor de licenças para emitir uma licença para o usuário.

O conteúdo criptografado está pronto para implantação e o cliente pode solicitar a licença do servidor.

O SDK fornece uma API Java para realizar essas tarefas, e inclui implementações de referência do servidor de licença e ferramentas de linha de comando baseadas nas APIs do Java. Para obter informações, consulte *Uso das implementações* de referência do Adobe Access.

## Novidades do Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK** externo: A capacidade de integrar um Content Key Management System (CKMS) ao serviço de licença do DRM e aos workflows de empacotamento de conteúdo, em vez de criptografar o CEK e agrupá-lo nos metadados do conteúdo. Consulte Visão geral [do CEK externo do DRM do](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)Adobe Access.

* **Devolução** de licença (comprovante): A capacidade de um cliente retornar (ou excluir) uma licença emitida para o cliente.
* **Servidor** de Chave Xbox: A capacidade de proteger o conteúdo enviado para o Xbox e o Xbox 360. (Um cliente Adobe Primetime é necessário.)

## Regras de uso personalizadas {#custom-usage-rules}

Especifica regras de uso personalizadas. Os dados personalizados podem ser incluídos nas licenças emitidas pelo License Server. A interpretação/tratamento desses dados depende totalmente da implementação do aplicativo cliente e do servidor de licenças.

Exemplo de caso de uso: Permite a extensibilidade das regras de uso, permitindo que outras regras comerciais sejam transmitidas com segurança como parte da política e/ou da licença de conteúdo. Por motivos de segurança, como essas regras de uso são aplicadas no código personalizado do aplicativo cliente, essa opção deve ser usada juntamente com as opções de lista de permissões do aplicativo AIR ou Flash Player SWF. Para obter mais informações, consulte Restrições [de tempo de](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md)execução e aplicativo.
