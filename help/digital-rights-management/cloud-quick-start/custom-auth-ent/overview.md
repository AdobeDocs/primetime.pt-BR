---
title: Visão geral do BEES
description: Visão geral do BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Visão geral do BEES{#bees-overview}

Você pode implementar um Serviço de Direitos de Back-end (BEES) para fornecer direitos personalizados para a operação de DRM da Primetime Cloud.

O DRM da Primetime Cloud usa a entrega de licença anônima por padrão. Isso significa que todas as solicitações de licença enviadas para o DRM da Primetime Cloud retornarão uma licença válida sem executar qualquer verificação adicional de autenticação/autorização (a menos que você tenha aplicado uma restrição de política que faça chamadas para usar a autenticação da Adobe Primetime).

A solicitação de licença contém a política de DRM que foi empregada durante o empacotamento / criptografia do conteúdo. A política de DRM é usada para gerar a licença de DRM retornada ao cliente. No cenário padrão, você deve tomar todas as decisões da política de DRM no momento do empacotamento do conteúdo. Os clientes que desejam ter mais controle sobre esses fluxos de trabalho têm as seguintes opções:

1. Integre a autenticação do Primetime para adicionar verificações de direito extras antes da reprodução.
1. Crie um serviço de direito local que o Primetime Cloud DRM consultará antes de permitir que qualquer dispositivo reproduza o conteúdo empacotado.

Seu serviço de direito local deve fornecer uma resposta ao DRM da Primetime Cloud que inclua os dois dados a seguir:

* `isAllowed`
* `drmPolicyToUse`

Eles determinam se um dispositivo tem permissão para reproduzir o conteúdo e qual política de DRM usar para gerar a licença de DRM (se `isAllowed` for verdadeiro).

Este documento aborda o que você precisa fazer para realizar a Opção 2 acima: Implemente seu próprio serviço de direito externo local e disponibilize-o ao Primetime Cloud DRM para conteúdo empacotado.
