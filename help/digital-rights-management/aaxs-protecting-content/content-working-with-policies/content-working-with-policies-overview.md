---
seo-title: Visão geral
title: Visão geral
uuid: 7363d241-6947-4a9c-80e5-e50be71066b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Visão geral {#overview}

Usando o Adobe® Access™, os provedores de conteúdo podem aplicar políticas a arquivos de mídia. Usando as APIs de gerenciamento de políticas, os administradores podem criar, visualização e atualizar políticas.

Uma *policy* define como os usuários podem visualização conteúdo; é uma coleção de informações que inclui configurações de segurança, requisitos de autenticação e direitos de uso. Quando as políticas são aplicadas, a criptografia e a assinatura permitem que os provedores de conteúdo mantenham o controle de seu conteúdo, independentemente do tamanho da distribuição. Os arquivos protegidos podem ser entregues usando o Adobe® Flash® Media Server ou um servidor HTTP. Eles podem ser baixados e reproduzidos em players personalizados criados com Adobe® AIR®, Adobe® Flash® Player e Adobe® Primetime SDK para iOS. A política é um modelo a ser usado pelo servidor de licenças ao gerar uma licença. O cliente também pode consultar a política antes de solicitar uma licença para determinar se precisa solicitar que o usuário se autentique antes de emitir uma solicitação de licença ao servidor.

Uma política especifica um ou mais direitos que são concedidos ao cliente. Normalmente, uma política inclui, no mínimo, o &quot;Play Right&quot;. Também é possível especificar vários Direitos de Reprodução, cada um com restrições diferentes. Quando o cliente encontra uma licença com vários Direitos de reprodução, usa a primeira licença para a qual atende a todas as restrições. Por exemplo, esse recurso pode ser usado para impor diferentes configurações de proteção de saída em diferentes plataformas. Para obter um exemplo de código ilustrando este exemplo, consulte `CreatePolicyWithOutputProtection.java` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.

É possível realizar as seguintes tarefas usando as APIs de gerenciamento de políticas:

* Criar e atualizar políticas
* Detalhes da política de visualização
* Gerenciar listas de atualização de política

Para obter detalhes sobre a API Java discutida neste capítulo, consulte *Referência da API de acesso ao Adobe*.

Para obter informações sobre a implementação de referência do Gerenciador de políticas, consulte *Usando as Implementações de referência de acesso a Adobe*.
