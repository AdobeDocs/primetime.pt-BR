---
title: Visão geral
description: Visão geral
copied-description: true
exl-id: 15733120-b1bb-46a7-90d2-4eb11c539d62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Visão geral  {#overview}

Com o Adobe® Access™, os provedores de conteúdo podem aplicar políticas aos arquivos de mídia. Usando as APIs de gerenciamento de políticas, os administradores podem criar, exibir detalhes e atualizar políticas.

A *política* define como os usuários podem visualizar o conteúdo; é uma coleção de informações que inclui configurações de segurança, requisitos de autenticação e direitos de uso. Quando as políticas são aplicadas, a criptografia e a assinatura permitem que os provedores de conteúdo mantenham o controle de seu conteúdo independentemente da amplitude da distribuição. Os arquivos protegidos podem ser entregues usando o Adobe® Flash® Media Server ou um servidor HTTP. Eles podem ser baixados e reproduzidos em reprodutores personalizados criados com o Adobe® AIR®, o Adobe® Flash® Player e o Adobe® Primetime SDK para iOS. A política é um modelo a ser usado pelo servidor de licença ao gerar uma licença. O cliente também pode consultar a política antes de solicitar uma licença para determinar se precisa solicitar que o usuário faça autenticação antes de emitir uma solicitação de licença para o servidor.

Uma política especifica um ou mais direitos concedidos ao cliente. Normalmente, uma política inclui, no mínimo, o &quot;Direito de reprodução&quot;. Também é possível especificar vários direitos de reprodução, cada um com restrições diferentes. Quando o cliente encontra uma licença com vários direitos de reprodução, ele usa a primeira para a qual atende a todas as restrições. Por exemplo, esse recurso pode ser usado para aplicar diferentes configurações de proteção de saída em diferentes plataformas. Para obter o código de exemplo que ilustra este exemplo, consulte `CreatePolicyWithOutputProtection.java` no diretório &quot;samples&quot; de Ferramentas de linha de comando de implementação de referência.

Você pode realizar as seguintes tarefas usando as APIs de gerenciamento de políticas:

* Criar e atualizar políticas
* Exibir detalhes da política
* Gerenciar listas de atualização de política

Para obter detalhes sobre a API Java discutida neste capítulo, consulte *Referência da API de acesso do Adobe*.

Para obter informações sobre a implementação de referência do Policy Manager, consulte *Uso das implementações de referência de acesso ao Adobe*.
