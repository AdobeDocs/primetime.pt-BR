---
title: Visão geral do BEES
description: Visão geral do BEES
copied-description: true
exl-id: 481af72b-40a3-4f33-9e91-990dc5308596
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Visão geral do BEES{#bees-overview}

Você pode implementar um Serviço de direitos de back-end (BEES) para fornecer direitos personalizados para a operação de DRM do Primetime Cloud.

O DRM do Primetime Cloud usa a entrega de licença anônima por padrão. Isso significa que todas as solicitações de licença enviadas ao Primetime Cloud DRM retornarão uma licença válida sem executar verificações de autenticação/autorização adicionais (a menos que você tenha aplicado uma restrição de política que exija o uso da autenticação da Adobe Primetime).

A solicitação de licença contém a política de DRM que foi empregada durante o empacotamento/criptografia do conteúdo. A política DRM é usada para gerar a licença DRM retornada ao cliente. No cenário padrão, é necessário tomar todas as decisões de política de DRM no momento do empacotamento do conteúdo. Os clientes que desejam ter mais controle sobre esses fluxos de trabalho têm as seguintes opções:

1. Integre a autenticação do Primetime para adicionar verificações de direito adicionais antes da reprodução.
1. Crie um serviço de direito local que o Primetime Cloud DRM consultará antes de permitir que qualquer dispositivo reproduza o conteúdo que você empacotou.

Seu serviço de direitos no local deve fornecer uma resposta ao Primetime Cloud DRM que inclui os dois dados a seguir:

* `isAllowed`
* `drmPolicyToUse`

Eles determinam se um dispositivo tem permissão para reproduzir o conteúdo e qual política de DRM usar para gerar a licença de DRM (se `isAllowed` é verdadeiro).

Este documento aborda o que você precisa fazer para realizar a Opção 2 acima: implementar seu próprio serviço de direitos externos no local e disponibilizá-lo para o Primetime Cloud DRM para o conteúdo que você empacotou.
