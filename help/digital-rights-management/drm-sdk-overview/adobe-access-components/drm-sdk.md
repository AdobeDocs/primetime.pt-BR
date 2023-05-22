---
description: Os principais componentes do Primetime DRM consistem em um SDK Java e nos ambientes de tempo de execução de cliente do Flash Player e do Adobe AIR.
title: SDK do Java, Flash Player e cliente Adobe AIR
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# SDK do Adobe Primetime DRM {#section_522E57DFEEFF4794978FF2D366B83690}

O DRM do Primetime é fornecido como um SDK Java que fornece os elementos fundamentais a partir dos quais você pode criar uma implementação de servidor. Usando o SDK, você pode criar uma solução de DRM do Primetime adequada ao modelo de negócios da sua organização.

As APIs Java fornecidas no SDK estão descritas nas subseções a seguir.

## APIs Java para gerenciar domínios de grupos de dispositivos{#java-apis-for-managing-device-group-domains}

Essas APIs são usadas para permitir que o servidor manipule solicitações de clientes para ingressar e sair de domínios de grupos de dispositivos.

Um domínio de grupo de dispositivos é uma coleção lógica de dispositivos que podem compartilhar licenças entre si. Para que isso aconteça, cada dispositivo deve primeiro ingressar/registrar no mesmo domínio. O SDK do DRM do Primetime, em execução em um servidor, deve lidar com as solicitações de ingresso (registro) no Domínio do dispositivo, bem como com as solicitações de licença (cancelamento de registro) do Domínio do dispositivo. Os dispositivos que não ingressaram em nenhum domínio receberão licenças vinculadas a esse dispositivo, que não podem ser compartilhadas com nenhum outro dispositivo.

## APIs Java para proteção de conteúdo{#java-apis-for-protecting-content}

Essas APIs são usadas para definir direitos e preparar conteúdo para distribuição. As APIs de proteção de conteúdo são:

* Gerenciamento de políticas

   A API de gerenciamento de política é usada para criar e modificar políticas a serem aplicadas ao conteúdo. As políticas podem ser criadas ou atualizadas, incluindo a obtenção/configuração de todas as regras de uso e a permissão de parâmetros adicionais em um namespace personalizado.

* Empacotamento de conteúdo

   A API de pacote de conteúdo é usada para criptografar o conteúdo e recuperar metadados do conteúdo do pacote.

## APIs Java para emissão de licenças{#java-apis-for-issuing-licenses}

Essas APIs são usadas quando um cliente solicita uma licença do servidor. O SDK é compatível com as seguintes solicitações do cliente:

* Autenticação

   A API de autenticação pode ser usada para lidar com solicitações de autenticação e gerar tokens de autenticação.

* Geração e aquisição de licença

   A API de geração e aquisição de licença é usada para gerar uma licença para o usuário.

* Suporte para clientes e conteúdo do Adobe AIR versão 1.5

   Para fins de compatibilidade com versões anteriores, o SDK tem APIs para lidar com solicitações de aplicativos do AIR criadas para uso com clientes AIR versão 1.5 e anteriores e conteúdo protegido.

## Implementação de referência {#reference-implementation}

O SDK inclui uma implementação de referência, uma simples implantação do Adobe Primetime DRM que demonstra como usar as APIs do Java. A implementação de referência fornece um License Server, um empacotador de pastas monitoradas, um aplicativo do Primetime DRM Manager AIR e ferramentas de linha de comando para empacotamento de conteúdo e gerenciamento de políticas com base nas APIs Java. Para saber mais sobre a implementação da referência de DRM do Primetime, consulte Proteção de conteúdo.
