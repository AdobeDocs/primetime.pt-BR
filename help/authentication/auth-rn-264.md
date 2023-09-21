---
title: Notas de versão da autenticação do Adobe Primetime 2.64
description: Notas de versão da autenticação do Adobe Primetime 2.64
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Notas de versão da autenticação do Adobe Primetime 2.64 {#authn-264-rn}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

Esta página descreve novos recursos, alterações e problemas conhecidos com esta versão:

## Lado do servidor e clientes da Web {#ss-web-clients}

* [Número da Build](#build-no-264)
* [Novos recursos](#new-featres-264)
* [Correções de erros](#bug-fixes-264)


### Número da Build {#build-no-264}

Autenticação do Adobe Primetime: adobe-pass-**2,64**

Data de lançamento: **08/11/2022 - 10/11/2022**

### Novos recursos {#new-featres-264}

* Atualizações da infraestrutura, destinadas a reduzir os tempos de resposta do servidor, melhorando o desempenho geral do sistema.
* Melhorias no novo mecanismo de identificação da plataforma.
* Capacidade de bloquear respostas de autenticação não solicitadas de MVPDs em que o parâmetro &quot;in_response_to&quot; está ausente da asserção SAML.

### Correções de erros {#bug-fixes-264}

* Correção da formatação incorreta de alguns tokens TempPass herdados.
* Problemas secundários foram solucionados no fluxo de autenticação da segunda tela.
