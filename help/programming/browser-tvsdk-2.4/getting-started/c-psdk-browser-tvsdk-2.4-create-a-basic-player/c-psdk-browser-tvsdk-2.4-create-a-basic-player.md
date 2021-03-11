---
description: Para usar o Browser TVSDK, você deve criar e configurar um reprodutor básico. Para reproduzir o conteúdo de vídeo, você pode criar um reprodutor básico de qualquer uma das duas maneiras usando o TVSDK do navegador ou usando a Estrutura da interface do usuário.
title: Jogador básico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Visão geral {#basic-player-overview}

Para usar o Browser TVSDK, você deve criar e configurar um reprodutor básico. Para reproduzir o conteúdo de vídeo, você pode criar um reprodutor básico de uma das duas maneiras: usando o TVSDK do navegador ou a Estrutura da interface do usuário.

## Uso do TVSDK do navegador {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Use as APIs fornecidas com o Browser TVSDK diretamente para codificar o player de vídeo. O SDK fornece estruturas e utilitários, bem como um reprodutor de referência para trabalhar.

>[!TIP]
>
>Para ver isso funcionando em um reprodutor de referência, não especifique nenhum atributo com `videoDiv`.

## Uso da estrutura da interface {#section_AE02384CFEF64A448C108232AB62A9FF}

Esse módulo é usado para criar instâncias do reprodutor, onde cada instância é vinculada a um elemento DOM (document object model) fornecido pelo chamador. Além de ter uma instância do TVSDK do Navegador, cada instância do reprodutor hospeda vários controles que compõem a interface do usuário do reprodutor.

A execução de cada controlo consiste em dois aspectos:

* Um `HTMLElement`, que é a representação visual do componente na tela
* Um `Behavior`, que gerencia o `HTMLElement` e fornece uma API para interações

Os detalhes sobre esses controles são fornecidos ao `VideoPlayer` usando um objeto de configuração, que é transmitido ao reprodutor em sua instanciação. Por padrão, cada componente forma uma hierarquia de objetos, com o elemento sendo fornecido à instância do reprodutor na raiz da árvore. À medida que cada componente é criado, ele é adicionado ao DOM no local apropriado.

Cada componente tem um nome, que é sua chave no objeto de configuração quando o objeto é registrado. A classe CSS do elemento DOM subjacente é formada como um prefixo `vp-` que é adicionado ao nome do componente.

Os componentes podem ser estendidos ou substituídos, sua configuração pode ser alterada e as propriedades iniciais podem ser definidas. Isso permite ter controle maior sobre as propriedades da API, o nome da classe CSS e, opcionalmente, os aspectos da implementação do componente. Essas opções podem ser usadas para personalizar a funcionalidade e permitir várias instâncias de um componente que pode ser estilizado ou configurado individualmente.

Todas as instâncias de componente podem ser acessadas com a propriedade `.behaviors` . As instâncias podem ser ativadas e desativadas e exibidas ou ocultas. Mas, uma vez que as instâncias são criadas, essas instâncias não podem ser removidas.
