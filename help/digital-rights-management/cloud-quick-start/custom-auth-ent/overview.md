---
seo-title: Visão geral do BEES
title: Visão geral do BEES
uuid: c6ee7528-fdfa-4a56-bea2-a5e2dab6d428
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Visão geral do BEES{#bees-overview}

Você pode implementar um serviço de direito de back-end (BEES) para fornecer direitos personalizados para a operação de DRM da Primetime Cloud.

Por padrão, a DRM da Primetime Cloud usa delivery de licença anônimo. Isso significa que todas as solicitações de licença enviadas para o DRM da Primetime Cloud retornarão uma licença válida sem executar verificações adicionais de autenticação/autorização (a menos que você tenha aplicado uma restrição de política que solicite o uso da autenticação do Adobe Primetime).

A solicitação de licença contém a política de DRM usada durante o empacotamento/criptografia do conteúdo. A política DRM é usada para gerar a licença DRM retornada ao cliente. No cenário padrão, você deve tomar todas as decisões de política de DRM no momento do empacotamento do conteúdo. Os clientes que desejam um controle mais preciso sobre esses workflows têm as seguintes opções:

1. Integre a autenticação Primetime para adicionar verificações de direito extras antes da reprodução.
1. Crie um serviço de direito local que o Primetime Cloud DRM query antes de permitir que qualquer dispositivo reproduza o conteúdo que você empacotou.

Seu serviço de direito local deve fornecer uma resposta ao DRM da Primetime Cloud que inclui os dois dados a seguir:

* `isAllowed`
* `drmPolicyToUse`

Eles determinam se um dispositivo tem permissão para reproduzir o conteúdo e qual política de DRM deve ser usada para gerar a licença de DRM (se `isAllowed` for verdadeiro).

Este documento aborda o que você precisa fazer para executar a Opção 2 acima: Implemente seu próprio serviço de direito externo local e disponibilize-o para o Primetime Cloud DRM para conteúdo que você empacotou.
