---
description: Os principais componentes do Primetime DRM consistem em um Java SDK e nos ambientes de tempo de execução do cliente Flash Player e do Adobe AIR.
seo-description: Os principais componentes do Primetime DRM consistem em um Java SDK e nos ambientes de tempo de execução do cliente Flash Player e do Adobe AIR.
seo-title: Java SDK, Flash Player e cliente Adobe AIR
title: Java SDK, Flash Player e cliente Adobe AIR
uuid: e6daed27-3803-4ef7-ba25-4a180af7502f
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

O Primetime DRM é fornecido como um Java SDK que fornece os blocos componentes a partir dos quais você pode criar uma implementação de servidor. Usando o SDK, você pode criar uma solução Primetime DRM adequada ao modelo de negócios de sua organização.

As APIs Java fornecidas no SDK são descritas nas subseções a seguir.

## APIs Java para gerenciar domínios de grupos de dispositivos{#java-apis-for-managing-device-group-domains}

Essas APIs são usadas para permitir que o servidor manipule solicitações de clientes para ingressar e sair de domínios de grupos de dispositivos.

Um domínio de grupo de dispositivos é uma coleção lógica de dispositivos que podem compartilhar licenças entre si. Para que isso ocorra, cada dispositivo deve primeiro se conectar/registrar no mesmo domínio. O SDK do DRM Primetime, em execução em um servidor, deve lidar com as solicitações de ingresso (registro) do domínio do dispositivo, bem como com solicitações de licença do domínio do dispositivo (cancelamento de registro). Os dispositivos que não estão associados a nenhum domínio receberão licenças que estão vinculadas a esse dispositivo, que não podem ser compartilhadas com nenhum outro dispositivo.

## APIs Java para proteção de conteúdo{#java-apis-for-protecting-content}

Essas APIs são usadas para definir direitos e preparar conteúdo para distribuição. As APIs de proteção de conteúdo são:

* Gerenciamento de políticas

   A API de gerenciamento de políticas é usada para criar e modificar políticas a serem aplicadas ao conteúdo. As políticas podem ser criadas ou atualizadas, incluindo obter/definir todas as regras de uso e permitir parâmetros adicionais em um namespace personalizado.

* Embalagem do conteúdo

   A API de empacotamento de conteúdo é usada para criptografar conteúdo e recuperar metadados do conteúdo empacotado.

## APIs Java para emissão de licenças{#java-apis-for-issuing-licenses}

Essas APIs são usadas quando um cliente solicita uma licença do servidor. O SDK oferece suporte às seguintes solicitações do cliente:

* Autenticação

   A API de autenticação pode ser usada para manipular solicitações de autenticação e gerar tokens de autenticação.

* Geração e aquisição de licenças

   A API de geração e aquisição de licença é usada para gerar uma licença para o usuário.

* Suporte para clientes e conteúdo do Adobe AIR versão 1.5

   Para fins de compatibilidade com versões anteriores, o SDK tem APIs para lidar com solicitações de aplicativos AIR criados para uso com clientes AIR versão 1.5 e anteriores e conteúdo protegido.

## Execução de referência {#reference-implementation}

O SDK inclui uma implementação de referência, uma implementação DRM simples do Adobe Primetime que demonstra como usar as APIs Java. A implementação de referência fornece um License Server, Watched Folder Packager, um aplicativo do Primetime DRM Manager AIR e ferramentas de linha de comando para empacotamento de conteúdo e gerenciamento de políticas com base nas APIs do Java. Para saber mais sobre a implementação de referência do DRM Primetime, consulte Proteger conteúdo.