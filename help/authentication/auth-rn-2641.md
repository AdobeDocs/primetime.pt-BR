---
title: Notas de versão da autenticação da Adobe Primetime 2.64.1
description: Notas de versão da autenticação da Adobe Primetime 2.64.1
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Notas de versão da autenticação da Adobe Primetime 2.64.1 {#authn-264-rn}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Esta página descreve novos recursos, alterações e problemas conhecidos com esta versão:

## Lado do servidor e clientes da Web {#server-side-web-clients-2641}

* [Número da build](#build-number-2641)
* [Visão geral da versão](#release-overview-2641)

### Número da build {#build-number-2641}

Autenticação Adobe Primetime: adobe-pass-**2.64.1.**
Data de lançamento: **31/01/2023 - 02/02/2023**

### Visão geral da versão {#release-overview-2641}

Esta versão adiciona o seguinte:

* A capacidade de bloquear respostas de autenticação não solicitadas de MVPDs nas quais o parâmetro &quot;in_response_to&quot; está ausente da asserção de SAML.
* Uma validação aprimorada do parâmetro redirect_url para estar em conformidade com os requisitos de segurança.
* Um registro aprimorado das informações do dispositivo para solicitações de autenticação de segunda tela, usando as informações fornecidas do dispositivo inicial.
