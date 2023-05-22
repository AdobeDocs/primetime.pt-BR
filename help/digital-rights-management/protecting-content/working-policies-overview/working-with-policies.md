---
title: Visão geral do trabalho com políticas de DRM
description: Visão geral do trabalho com políticas de DRM
copied-description: true
exl-id: 734d0be3-2abe-400c-bc34-00046ec52f4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Visão geral {#working-with-drm-policies-overview}

Os provedores de conteúdo podem aplicar políticas de DRM a arquivos de mídia usando o SDK de DRM do Primetime. Em seguida, os administradores podem criar, exibir detalhes e atualizar políticas de DRM usando APIs de gerenciamento de políticas.

A *`DRM policy`* O é uma coleção de informações que inclui configurações de segurança, requisitos de autenticação e direitos de uso. A política define como os usuários podem visualizar o conteúdo. As políticas, a criptografia e a assinatura DRM permitem que os provedores de conteúdo mantenham o controle de seu conteúdo, independentemente da amplitude da distribuição do conteúdo.

Uma política DRM serve como um modelo que o servidor de licenças usa ao gerar uma licença. Um cliente também pode consultar a política DRM antes de solicitar uma licença, para determinar se o cliente precisa solicitar a autenticação do usuário antes de emitir uma solicitação de licença para o servidor.

Você pode fornecer conteúdo protegido usando o Flash Media Server Adobe ou um servidor HTTP. Os usuários podem baixar e reproduzir conteúdo protegido em players personalizados criados com o SDK DRM do Primetime.

Uma política DRM especifica um ou mais direitos concedidos ao cliente. Normalmente, uma política de DRM inclui, no mínimo, a *`Play Right`*. Você também pode especificar vários direitos de reprodução, cada um com restrições diferentes. Quando o cliente recebe uma licença com vários direitos de reprodução, ele usa a primeira licença que atende a todas as restrições. Por exemplo, você pode aplicar diferentes configurações de proteção de saída em diferentes plataformas.

Consulte `CreatePolicyWithOutputProtection.java` nas Ferramentas de linha de comando da Implementação de referência [!DNL samples] diretório do código de exemplo que ilustra este exemplo.

Você pode concluir as seguintes tarefas com as APIs de gerenciamento de política do Primetime DRM:

* Criar e atualizar políticas
* Exibir detalhes da política de DRM
* Gerenciar listas de atualização de política DRM

Consulte a *Referência da API DRM do Primetime* para obter detalhes sobre a API do Java.

Consulte a *Uso das implementações de referência de DRM do Primetime* guia para obter informações sobre o Gerenciador de políticas DRM do Primetime.
