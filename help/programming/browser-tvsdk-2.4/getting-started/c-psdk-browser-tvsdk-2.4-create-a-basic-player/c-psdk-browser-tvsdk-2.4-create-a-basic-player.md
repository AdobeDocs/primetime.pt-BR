---
description: Para usar o TVSDK do navegador, você deve criar e configurar um reprodutor básico. Para reproduzir conteúdo de vídeo, você pode criar um reprodutor básico de duas maneiras usando o TVSDK do navegador ou usando a Estrutura da interface do usuário.
title: Reprodutor básico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Visão geral {#basic-player-overview}

Para usar o TVSDK do navegador, você deve criar e configurar um reprodutor básico. Para reproduzir conteúdo de vídeo, você pode criar um reprodutor básico de duas maneiras: usando o TVSDK do navegador ou usando a Estrutura da interface do usuário.

## Utilização do TVSDK do navegador {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Use as APIs fornecidas com o TVSDK do navegador diretamente para codificar seu reprodutor de vídeo. O SDK fornece estruturas e utilitários, bem como um player de referência para trabalhar.

>[!TIP]
>
>Para ver isso funcionando em um reprodutor de referência, não especifique atributos com `videoDiv`.

## Uso da estrutura da interface do usuário {#section_AE02384CFEF64A448C108232AB62A9FF}

Esse módulo é usado para criar instâncias do reprodutor, em que cada instância é vinculada a um elemento DOM (document object model) fornecido pelo chamador. Além de ter uma instância do TVSDK do navegador, cada instância do player hospeda vários controles que compõem a interface do usuário do player.

A implementação de cada controle consiste em dois aspectos:

* Um `HTMLElement`, que é a representação visual do componente na tela
* A `Behavior`, que gerencia a `HTMLElement` e fornece uma API para interações

Os detalhes sobre esses controles são fornecidos ao `VideoPlayer` usando um objeto de configuração, que é passado para o reprodutor em sua instanciação. Por padrão, cada componente forma uma hierarquia de objetos, com o elemento sendo fornecido à instância do player na raiz da árvore. À medida que cada componente é criado, ele é adicionado ao DOM no local apropriado.

Cada componente tem um nome, que é sua chave no objeto de configuração quando o objeto é registrado. A classe CSS do elemento DOM subjacente é formada como um `vp-` prefixo adicionado ao nome do componente.

Os componentes podem ser estendidos ou substituídos, sua configuração pode ser alterada e as propriedades iniciais definidas. Isso permite ter maior controle sobre as propriedades da API, o nome da classe CSS e, opcionalmente, os aspectos da implementação do componente. Essas opções podem ser usadas para personalizar a funcionalidade e permitir várias instâncias de um componente que pode ser estilizado ou configurado individualmente.

Todas as instâncias de componentes podem ser acessadas com o `.behaviors` propriedade. As instâncias podem ser ativadas e desativadas e exibidas ou ocultas. Mas, uma vez que as instâncias são criadas, elas não podem ser removidas.
