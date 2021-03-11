---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Visão geral {#overview}

Usando o Adobe® Access™, os provedores de conteúdo podem aplicar políticas a arquivos de mídia. Usando as APIs de gerenciamento de políticas, os administradores podem criar, exibir detalhes e atualizar políticas.

Uma *política* define como os usuários podem visualizar conteúdo; é uma coleção de informações que inclui configurações de segurança, requisitos de autenticação e direitos de uso. Quando as políticas são aplicadas, a criptografia e a assinatura permitem que os provedores de conteúdo mantenham o controle de seu conteúdo, independentemente de qual seja a distribuição. Os arquivos protegidos podem ser entregues usando o Adobe® Flash® Media Server ou um servidor HTTP. Eles podem ser baixados e reproduzidos em players personalizados criados com Adobe® AIR®, Flash® Player e Adobe® Primetime SDK para iOS. A política é um template para o servidor de licenças usar ao gerar uma licença. O cliente também pode consultar a política antes de solicitar uma licença para determinar se é necessário solicitar que o usuário se autentique antes de emitir uma solicitação de licença para o servidor.

Uma política especifica um ou mais direitos que são concedidos ao cliente. Normalmente, uma política inclui, no mínimo, o &quot;Direito de reprodução&quot;. Também é possível especificar vários Direitos de reprodução, cada um com diferentes restrições. Quando o cliente encontra uma licença com vários Direitos de reprodução, ele usa a primeira para a qual atende a todas as restrições. Por exemplo, esse recurso pode ser usado para impor diferentes configurações de proteção de saída em plataformas diferentes. Para obter um código de amostra ilustrando este exemplo, consulte `CreatePolicyWithOutputProtection.java` no diretório &quot;samples&quot; de Ferramentas de Linha de Comando de Implementação de Referência.

Você pode realizar as seguintes tarefas usando as APIs de gerenciamento de políticas:

* Criar e atualizar políticas
* Exibir detalhes da política
* Gerenciar listas de atualização de política

Para obter detalhes sobre a API do Java discutida neste capítulo, consulte *Referência da API de acesso ao Adobe*.

Para obter informações sobre a implementação de referência do Gerenciador de Políticas, consulte *Usando as Implementações de Referência do Acesso ao Adobe*.
