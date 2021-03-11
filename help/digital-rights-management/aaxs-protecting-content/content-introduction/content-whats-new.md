---
description: 'O Adobe® Access™ é uma solução avançada de gestão de direitos digitais e proteção de conteúdo para conteúdos audiovisuais de alto valor. Usando as ferramentas criadas usando as APIs do Java, você pode criar políticas, aplicar políticas a arquivos contendo conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes '
title: Visão geral
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Visão geral {#overview}

O Adobe® Access™ é uma solução avançada de gestão de direitos digitais e proteção de conteúdo para conteúdos audiovisuais de alto valor. Usando as ferramentas criadas usando as APIs do Java, você pode criar políticas, aplicar políticas a arquivos contendo conteúdo de áudio e vídeo e criptografar esses arquivos. As etapas de alto nível para executar essas tarefas são as seguintes:

1. Use as APIs do Java para definir as propriedades da política e os parâmetros de criptografia.
1. Crie uma política descrevendo as funções de uso do conteúdo. (Consulte [Trabalhar com políticas](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Você pode criar qualquer número de políticas. A maioria dos usuários cria um pequeno número de políticas e as aplica a muitos arquivos.

1. Compacte um arquivo de mídia.

   Neste contexto, *empacotar um arquivo* significa criptografá-lo e aplicar uma política a ele. (Consulte [Empacotando arquivos de mídia](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implemente o servidor de licenças para emitir uma licença para o usuário.

O conteúdo criptografado agora está pronto para implantação e o cliente pode solicitar a licença do servidor.

O SDK fornece uma API Java para realizar essas tarefas e inclui implementações de referência do servidor de licença e ferramentas de linha de comando baseadas nas APIs do Java. Para obter informações, consulte *Usando as implementações de referência de acesso ao Adobe*.

## Novidades no Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK** externo: A capacidade de integrar um Sistema de gerenciamento de chaves de conteúdo (CKMS) aos workflows de serviço de licenças de DRM e Pacotes de conteúdo, em vez de criptografar o CEK e agrupá-lo nos metadados do conteúdo. Consulte [Visão geral externa do CEK do DRM de acesso ao Adobe](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Devolução** de licença (comprovante): A capacidade de um cliente retornar (ou excluir) uma licença emitida para o cliente.
* **Servidor** de chaves Xbox: A capacidade de proteger o conteúdo enviado para o Xbox e o Xbox 360. (É necessário um cliente Adobe Primetime.)

## Regras de uso personalizadas {#custom-usage-rules}

Especifica regras de uso personalizadas. Os dados personalizados podem ser incluídos em licenças emitidas pelo License Server. A interpretação/tratamento desses dados depende totalmente da implementação do aplicativo cliente e do servidor de licenças.

Exemplo de caso de uso: Permite a extensibilidade das regras de uso, permitindo que outras regras de negócios sejam transmitidas com segurança como parte da política e/ou da licença de conteúdo. Por motivos de segurança, como essas regras de uso são aplicadas no código de aplicativo cliente personalizado, essa opção deve ser usada juntamente com as opções de lista de permissões do aplicativo AIR ou do Flash Player SWF. Para obter mais informações, consulte [Tempo de execução e restrições de aplicativo](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
