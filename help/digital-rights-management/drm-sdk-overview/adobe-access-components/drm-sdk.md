---
description: Os principais componentes do DRM do Primetime consistem em um SDK Java e nos ambientes de tempo de execução do cliente Flash Player e Adobe AIR.
title: SDK Java, cliente Flash Player e Adobe AIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Adobe Primetime DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

O DRM do Primetime é fornecido como um SDK Java que fornece os blocos de construção a partir dos quais você pode criar uma implementação de servidor. Usando o SDK, você pode criar uma solução de DRM do Primetime adequada ao modelo de negócios de sua organização.

As APIs Java fornecidas no SDK são descritas nas subseções a seguir.

## APIs Java para gerenciar domínios de grupos de dispositivos{#java-apis-for-managing-device-group-domains}

Essas APIs são usadas para permitir que o servidor manipule solicitações de clientes para ingressar e sair de domínios de grupos de dispositivos.

Um domínio de grupo de dispositivos é uma coleção lógica de dispositivos que podem compartilhar licenças entre si. Para que isso aconteça, cada dispositivo deve primeiro se associar/registrar no mesmo domínio. O SDK do DRM do Primetime, em execução em um servidor, deve lidar com as solicitações de associação (registro) do domínio do dispositivo, bem como com solicitações de licença (cancelamento de registro) do domínio do dispositivo. Os dispositivos que não estão associados a nenhum domínio receberão licenças vinculadas a esse dispositivo, que não podem ser compartilhadas com nenhum outro dispositivo.

## APIs Java para proteger conteúdo{#java-apis-for-protecting-content}

Essas APIs são usadas para definir direitos e preparar conteúdo para distribuição. As APIs de proteção de conteúdo são:

* Gerenciamento de políticas

   A API de gerenciamento de políticas é usada para criar e modificar políticas a serem aplicadas ao conteúdo. As políticas podem ser criadas ou atualizadas, incluindo a obtenção/configuração de todas as regras de uso e a permissão de parâmetros adicionais em um namespace personalizado.

* Embalagem do conteúdo

   A API de empacotamento de conteúdo é usada para criptografar conteúdo e recuperar metadados do conteúdo empacotado.

## APIs Java para emissão de licenças{#java-apis-for-issuing-licenses}

Essas APIs são usadas quando um cliente solicita uma licença do servidor. O SDK é compatível com as seguintes solicitações do cliente:

* Autenticação

   A API de autenticação pode ser usada para lidar com solicitações de autenticação e gerar tokens de autenticação.

* Geração e aquisição de licenças

   A API de geração e aquisição de licença é usada para gerar uma licença para o usuário.

* Suporte para clientes e conteúdo da versão 1.5 do Adobe AIR

   Para fins de compatibilidade com versões anteriores, o SDK tem APIs para lidar com solicitações de aplicativos AIR criadas para uso com o AIR versão 1.5 e clientes anteriores e conteúdo protegido.

## Implementação de referência {#reference-implementation}

O SDK inclui uma implementação de referência, uma implantação de DRM simples do Adobe Primetime que demonstra como usar as APIs do Java. A implementação de referência fornece um License Server, Watched Folder Packager, aplicativo AIR do Primetime DRM Manager e ferramentas de linha de comando para empacotamento de conteúdo e gerenciamento de políticas com base nas APIs Java. Para saber mais sobre a implementação de referência do DRM do Primetime, consulte Proteção de conteúdo.