---
description: O Adobe® Access™ é uma solução avançada de gerenciamento de direitos digitais e proteção de conteúdo para conteúdo audiovisual de alto valor. Usando ferramentas criadas com APIs Java, é possível criar políticas, aplicar políticas a arquivos com conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes
title: Visão geral
exl-id: cf081058-9b41-4b09-9258-a7d873799846
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Visão geral {#overview}

O Adobe® Access™ é uma solução avançada de gerenciamento de direitos digitais e proteção de conteúdo para conteúdo audiovisual de alto valor. Usando ferramentas criadas com APIs Java, é possível criar políticas, aplicar políticas a arquivos com conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes:

1. Use as APIs do Java para definir as propriedades da política e os parâmetros de criptografia.
1. Crie uma política que descreva as funções de uso do conteúdo. (Consulte [Trabalhar com políticas](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Você pode criar qualquer número de políticas. A maioria dos usuários cria um pequeno número de políticas e as aplica a muitos arquivos.

1. Compactar um arquivo de mídia.

   Neste contexto, *empacotando um arquivo* significa criptografá-la e aplicar uma política a ela. (Consulte [Empacotamento de arquivos de mídia](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implemente o servidor de licenças para emitir uma licença para o usuário.

O conteúdo criptografado agora está pronto para implantação e o cliente pode solicitar a licença do servidor.

O SDK fornece uma API Java para realizar essas tarefas e inclui implementações de referência do servidor de licenças e ferramentas de linha de comando baseadas nas APIs Java. Para obter informações, consulte *Uso das implementações de referência de acesso ao Adobe*.

## Novidades do Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK externo**: a capacidade de integrar um sistema de gerenciamento de chaves de conteúdo (CKMS) aos fluxos de trabalho de fornecimento de licenças e de empacotamento de conteúdo do DRM, em vez de criptografar o CEK e agrupá-lo nos metadados do conteúdo. Consulte [Visão geral do CEK externo de DRM de acesso ao Adobe](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Devolução de Licença (voucher)**: a capacidade de um cliente retornar (ou excluir) uma licença emitida para o cliente.
* **Servidor de Chaves Xbox**: a capacidade de proteger o conteúdo enviado ao Xbox e ao Xbox 360. (É necessário um cliente do Adobe Primetime.)

## Regras de uso personalizadas {#custom-usage-rules}

Especifica regras de uso personalizadas. Os dados personalizados podem ser incluídos em licenças emitidas pelo License Server. A interpretação/manuseio desses dados depende totalmente da implementação do aplicativo cliente e do servidor de licenças.

Exemplo de caso de uso: permite a extensibilidade das regras de uso, permitindo que outras regras de negócios sejam transmitidas com segurança como parte da política e/ou licença de conteúdo. Por motivos de segurança, como essas regras de uso são aplicadas no código de aplicativo cliente personalizado, essa opção deve ser usada juntamente com as opções de aplicativo AIR ou lista de permissões de Flash Player SWF. Para obter mais informações, consulte [Restrições de tempo de execução e de aplicativo](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
