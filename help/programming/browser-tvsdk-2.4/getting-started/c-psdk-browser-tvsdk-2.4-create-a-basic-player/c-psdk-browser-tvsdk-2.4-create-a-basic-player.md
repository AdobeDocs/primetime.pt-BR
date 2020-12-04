---
description: Para usar o TVSDK do navegador, você deve criar e configurar um player básico. Para reproduzir conteúdo de vídeo, você pode criar um player básico de duas maneiras usando o TVSDK do navegador ou usando a Estrutura da interface do usuário.
seo-description: Para usar o TVSDK do navegador, você deve criar e configurar um player básico. Para reproduzir conteúdo de vídeo, você pode criar um player básico de duas maneiras usando o TVSDK do navegador ou usando a Estrutura da interface do usuário.
seo-title: Jogador básico
title: Jogador básico
uuid: 44a27458-be12-452f-92b9-3cef79439257
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Visão geral {#basic-player-overview}

Para usar o TVSDK do navegador, você deve criar e configurar um player básico. Para reproduzir conteúdo de vídeo, você pode criar um player básico de duas maneiras: usando a TVSDK do navegador ou a Estrutura da interface do usuário.

## Usando o TVSDK do navegador {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Use as APIs fornecidas com o TVSDK do navegador diretamente para codificar seu player de vídeo. O SDK fornece estruturas e utilitários, bem como um player de referência para trabalhar.

>[!TIP]
>
>Para ver isso funcionando em um player de referência, não especifique nenhum atributo com `videoDiv`.

## Usar a estrutura da interface {#section_AE02384CFEF64A448C108232AB62A9FF}

Este módulo é usado para criar instâncias do player, onde cada instância é vinculada a um elemento DOM (Modelo de objeto de documento) fornecido pelo chamador. Além de ter uma instância do TVSDK do navegador, cada instância do player hospeda vários controles que compõem a interface do usuário para o player.

A execução de cada controlo consiste em dois aspectos:

* Uma `HTMLElement`, que é a representação visual do componente na tela
* Um `Behavior`, que gerencia o `HTMLElement` e fornece uma API para interações

Os detalhes sobre esses controles são fornecidos para `VideoPlayer` usando um objeto de configuração, que é passado para o player em sua instanciação. Por padrão, cada componente forma uma hierarquia de objetos, com o elemento sendo fornecido à instância do player na raiz da árvore. Conforme cada componente é criado, ele é adicionado ao DOM no local apropriado.

Cada componente tem um nome, que é sua chave no objeto de configuração quando o objeto é registrado. A classe CSS do elemento DOM subjacente é formada como um prefixo `vp-` que é adicionado ao nome do componente.

Os componentes podem ser estendidos ou substituídos, sua configuração pode ser alterada e as propriedades iniciais podem ser definidas. Isso permite que você tenha um controle maior sobre as propriedades da API, o nome da classe CSS e, opcionalmente, sobre os aspectos da implementação do componente. Essas opções podem ser usadas para personalizar a funcionalidade e permitir várias instâncias de um componente que pode ser estilizado ou configurado individualmente.

Todas as instâncias de componente podem ser acessadas com a propriedade `.behaviors`. As instâncias podem ser ativadas e desativadas e exibidas ou ocultas. No entanto, uma vez que as instâncias são criadas, elas não podem ser removidas.
