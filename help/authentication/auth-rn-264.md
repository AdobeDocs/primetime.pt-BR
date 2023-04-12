---
title: Notas de versão da autenticação da Adobe Primetime 2.64
description: Notas de versão da autenticação da Adobe Primetime 2.64
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Notas de versão da autenticação da Adobe Primetime 2.64 {#authn-264-rn}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Esta página descreve novos recursos, alterações e problemas conhecidos com esta versão:

## Lado do servidor e clientes da Web {#ss-web-clients}

* [Número da build](#build-no-264)
* [Novos recursos](#new-featres-264)
* [Correções de erros](#bug-fixes-264)


### Número da build {#build-no-264}

Autenticação Adobe Primetime: adobe-pass-**2,64**

Data de lançamento: **08/11/2022 - 11/10/2022**

### Novos recursos {#new-featres-264}

* Atualizações de infraestrutura, direcionadas para reduzir os tempos de resposta do servidor, melhorando o desempenho geral do sistema.
* Melhorias no novo mecanismo de identificação da plataforma.
* Capacidade de bloquear respostas de autenticação não solicitadas de MVPDs nas quais o parâmetro &quot;in_response_to&quot; está ausente da asserção de SAML.

### Correções de erros {#bug-fixes-264}

* Correção da formatação incorreta de alguns tokens TempPass herdados.
* Problemas secundários foram solucionados no fluxo de autenticação da segunda tela.
