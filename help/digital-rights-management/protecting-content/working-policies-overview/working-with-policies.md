---
seo-title: Como trabalhar com a visão geral das políticas de DRM
title: Como trabalhar com a visão geral das políticas de DRM
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Visão geral {#working-with-drm-policies-overview}

Os provedores de conteúdo podem aplicar políticas de DRM a arquivos de mídia usando o SDK do Primetime DRM. Os administradores podem criar, visualização e atualizar políticas de DRM usando APIs de gerenciamento de políticas.

Um *`DRM policy`* é uma coleção de informações que inclui configurações de segurança, requisitos de autenticação e direitos de uso. A política define como os usuários podem visualização conteúdo. As políticas, a criptografia e a assinatura do DRM permitem que os provedores de conteúdo mantenham o controle de seu conteúdo, independentemente do tamanho da distribuição do conteúdo.

Uma política DRM serve como um modelo que o servidor de licenças usa quando gera uma licença. Um cliente também pode consultar a política de DRM antes de solicitar uma licença, para determinar se o cliente precisa solicitar a autenticação do usuário antes de emitir uma solicitação de licença ao servidor.

Você pode fornecer conteúdo protegido usando um Flash Media Server Adobe ou um servidor HTTP. Os usuários podem baixar e reproduzir conteúdo protegido em players personalizados criados com o SDK do Primetime DRM.

Uma política de DRM especifica um ou mais direitos que são concedidos ao cliente. Normalmente, uma política de DRM inclui, no mínimo, *`Play Right`*. Você também pode especificar vários Direitos de reprodução, cada um com restrições diferentes. Quando o cliente recebe uma licença com vários Direitos de reprodução, usa a primeira licença que atende a todas as restrições. Por exemplo, você pode aplicar diferentes configurações de proteção de saída em diferentes plataformas.

Consulte `CreatePolicyWithOutputProtection.java` no diretório Reference Implementation Command Line Tools [!DNL samples] para obter exemplos de códigos que ilustram este exemplo.

Você pode concluir as seguintes tarefas com as APIs de gerenciamento de política do DRM Primetime:

* Criar e atualizar políticas
* Detalhes da política DRM de visualização
* Gerenciar listas de atualização da política DRM

Consulte *Referência da API DRM Primetime* para obter detalhes sobre a API Java.

Consulte o guia *Using the Primetime DRM Reference Implementations* para obter informações sobre o Primetime DRM Policy Manager.
