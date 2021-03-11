---
title: Como trabalhar com a visão geral das políticas de DRM
description: Como trabalhar com a visão geral das políticas de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Visão geral {#working-with-drm-policies-overview}

Os provedores de conteúdo podem aplicar políticas de DRM a arquivos de mídia usando o SDK de DRM do Primetime. Os administradores podem criar, exibir detalhes e atualizar políticas de DRM usando APIs de gerenciamento de políticas.

Um *`DRM policy`* é uma coleção de informações que inclui configurações de segurança, requisitos de autenticação e direitos de uso. A política define como os usuários podem visualizar conteúdo. As políticas, criptografia e assinatura de DRM permitem que os provedores de conteúdo mantenham o controle de seu conteúdo, independentemente da amplitude da distribuição do conteúdo.

Uma política de DRM serve como um modelo que o servidor de licenças usa ao gerar uma licença. Um cliente também pode consultar a política de DRM antes de solicitar uma licença, para determinar se ele precisa solicitar a autenticação do usuário antes de emitir uma solicitação de licença ao servidor.

Você pode fornecer conteúdo protegido usando o Adobe Flash Media Server ou um servidor HTTP. Os usuários podem baixar e reproduzir conteúdo protegido em players personalizados criados com o SDK DRM do Primetime.

Uma política de DRM especifica um ou mais direitos que são concedidos ao cliente. Normalmente, uma política de DRM inclui, no mínimo, o *`Play Right`*. Você também pode especificar vários Direitos de reprodução, cada um com diferentes restrições. Quando o cliente recebe uma licença com vários Direitos de reprodução, ele usa a primeira licença que atende a todas as restrições. Por exemplo, você pode impor diferentes configurações de proteção de saída em diferentes plataformas.

Consulte `CreatePolicyWithOutputProtection.java` no diretório Ferramentas de linha de comando da implementação de referência [!DNL samples] para obter o código de amostra que ilustra este exemplo.

Você pode concluir as seguintes tarefas com as APIs de gerenciamento de políticas de DRM do Primetime:

* Criar e atualizar políticas
* Exibir detalhes da política de DRM
* Gerenciar listas de atualização da política DRM

Consulte a *Referência da API DRM do Primetime* para obter detalhes sobre a API do Java.

Consulte o guia *Using the Primetime DRM Reference Implementations* para obter informações sobre o Gerenciador de políticas de DRM do Primetime.
