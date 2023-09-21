---
title: Regras de uso
description: Regras de uso
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Regras de uso {#usage-rules}

Os tópicos a seguir descrevem as regras de uso que podem ser especificadas em uma política do Adobe Primetime DRM.

## Autenticação do usuário {#user-authentication}

Autenticação de usuário especifica se uma credencial, como nome de usuário e senha, é necessária para adquirir uma licença. Se o licenciamento autenticado (baseado em identidade) for especificado, o servidor ~~_autentica_~~ usuário antes de emitir uma licença.

Exemplo de caso de uso: um serviço de assinatura pode exigir que um nome de usuário e uma senha sejam inseridos antes de emitir uma licença de conteúdo. Um DVD ou disco Blu-ray com cópia digital pode fornecer um código ou outro token como prova de pagamento, que pode ser resgatado para um download eletrônico.
