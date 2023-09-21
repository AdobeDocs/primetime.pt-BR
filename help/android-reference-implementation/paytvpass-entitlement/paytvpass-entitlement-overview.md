---
description: Você pode usar a autenticação do Adobe Primetime para gerenciar os direitos do usuário no seu reprodutor.
title: Visão geral
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Visão geral {#overview}

Você pode usar a autenticação do Adobe Primetime para gerenciar os direitos do usuário no seu reprodutor.

O gerenciador de recursos que encapsula os fluxos de direito de autenticação do Primetime é o `EntitlementManager`. Essa classe encapsula a lógica de direito enquanto delega o trabalho da interface do usuário para outro lugar.

Esta implementação de referência para Android usa a biblioteca AccessEnabler de autenticação do Primetime versão 1.7.3. Grande parte da implementação é muito semelhante ao aplicativo de demonstração existente fornecido com a biblioteca AccessEnabler.

Para obter informações adicionais sobre a autenticação do Primetime, consulte a documentação em [Introdução à integração do programador](https://tve.helpdocsonline.com/introduction-to-programmer-integration).
