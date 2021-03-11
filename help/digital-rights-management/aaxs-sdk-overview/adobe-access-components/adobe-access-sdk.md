---
description: Os principais componentes do Adobe Access consistem em um SDK Java e nos ambientes de tempo de execução do cliente Flash Player e Adobe AIR.
title: SDK Java, cliente Flash Player e Adobe AIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Componentes do Adobe Access{#adobe-access-components}

Os principais componentes do Adobe Access consistem em um SDK Java e nos ambientes de tempo de execução do cliente Flash Player e Adobe AIR.

Para obter mais informações sobre como configurar o SDK, consulte Configuração do SDK em *Uso do SDK de acesso do Adobe para proteção de conteúdo.*

O SDK de acesso ao Adobe permite desenvolver uma solução de gerenciamento de direitos digitais que se integra à infraestrutura de negócios existente de sua organização, como gerenciamento de conteúdo, faturamento e sistemas de controle de acesso do usuário. O Flash Player e o Adobe AIR permitem que você crie e implante facilmente aplicativos através dos quais os consumidores podem acessar e visualizar grandes bibliotecas de conteúdo digital.

## SDK de acesso ao Adobe {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

O Adobe Access é fornecido como um SDK Java que fornece os blocos de construção a partir dos quais você pode criar uma implementação de servidor. Usando o SDK, você pode criar uma solução de Acesso ao Adobe adequada ao modelo de negócios de sua organização.

As APIs Java fornecidas no SDK são descritas nas subseções a seguir.

## APIs Java para gerenciar domínios de grupos de dispositivos {#java-apis-for-managing-device-group-domains}

Essas APIs são usadas para permitir que o servidor manipule solicitações de clientes para ingressar e sair de domínios de grupos de dispositivos.

Um domínio de grupo de dispositivos é uma coleção lógica de dispositivos que podem compartilhar licenças entre si. Para que isso aconteça, cada dispositivo deve primeiro se associar/registrar no mesmo domínio. O SDK de acesso ao Adobe, em execução em um servidor, deve lidar com as solicitações de associação (registro) do domínio do dispositivo, bem como com solicitações de licença (cancelamento de registro) do domínio do dispositivo. Os dispositivos que não estão associados a nenhum domínio receberão licenças vinculadas a esse dispositivo, que não podem ser compartilhadas com nenhum outro dispositivo.

## APIs Java para proteger conteúdo {#java-apis-for-protecting-content}

Essas APIs são usadas para definir direitos e preparar conteúdo para distribuição. As APIs de proteção de conteúdo são:

* Gerenciamento de políticas

   A API de gerenciamento de políticas é usada para criar e modificar políticas a serem aplicadas ao conteúdo. As políticas podem ser criadas ou atualizadas, incluindo a obtenção/configuração de todas as regras de uso e a permissão de parâmetros adicionais em um namespace personalizado.

* Embalagem do conteúdo

   A API de empacotamento de conteúdo é usada para criptografar conteúdo e recuperar metadados do conteúdo empacotado.

## APIs Java para emissão de licenças {#java-apis-for-issuing-licenses}

Essas APIs são usadas quando um cliente solicita uma licença do servidor. O SDK é compatível com as seguintes solicitações do cliente:

* Autenticação

   A API de autenticação pode ser usada para lidar com solicitações de autenticação e gerar tokens de autenticação.

* Geração e aquisição de licenças

   A API de geração e aquisição de licença é usada para gerar uma licença para o usuário.

* Suporte para clientes e conteúdo da versão 1.5 do Adobe AIR

   Para fins de compatibilidade com versões anteriores, o SDK tem APIs para lidar com solicitações de aplicativos AIR criadas para uso com o AIR versão 1.5 e clientes anteriores e conteúdo protegido.

## Implementação de referência {#reference-implementation}

O SDK inclui uma implementação de referência, uma implantação de Adobe Access simples que demonstra como usar as APIs do Java. A implementação de referência fornece um License Server, Watched Folder Packager, um aplicativo AIR do Adobe Access Manager e ferramentas de linha de comando para empacotamento de conteúdo e gerenciamento de políticas com base nas APIs do Java. Para saber mais sobre a implementação de referência do Acesso ao Adobe, consulte *Proteção de Conteúdo*.

## Adobe Access Server para transmissão protegida {#adobe-access-server-for-protected-streaming}

Para casos de uso de transmissão em que o conteúdo é protegido com Adobe Access, como para Adobe HTTP Dynamic Streaming, o software também inclui Adobe Access Server for Protected Streaming. Essa solução pode ser facilmente implantada em um contêiner de servlet, como o Tomcat, e pode alcançar um alto nível de escalabilidade e desempenho para atender às maiores necessidades de distribuição de conteúdo.

## Flash Player Adobe {#adobe-flash-player}

O Flash Player é um plug-in leve de navegador e tempo de execução que fornece experiências de usuário consistentes e envolventes, reprodução impressionante de áudio/vídeo e alcance abrangente. O Flash Player oferece reprodução de alta qualidade de conteúdo de vídeo transmitido ou baixado. Para editores de conteúdo, o Flash Player fornece o meio de personalizar as telas de reprodução ao redor do conteúdo, permitindo experiências de marca e monetização mais profundas por meio de anúncios usando banners e sobreposições. Para os consumidores, o Flash Player apresenta uma maneira intuitiva e visualmente atraente para visualizar o conteúdo de vídeo.

Para obter mais informações sobre o Flash Player, visite: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

O Adobe AIR é um tempo de execução entre sistemas operacionais que permite que os produtores de conteúdo estendam seus investimentos existentes na Web para o desktop, criando aplicativos de multimídia personalizados. Baseado em tecnologias comprovadas e abertas, ele oferece uma maneira confiável e simplificada para que as empresas desenvolvam e implantem aplicativos personalizados confiáveis para oferecer uma experiência do usuário mais segura e agradável. O Adobe AIR permite que as empresas integrem facilmente mídia avançada para criar uma experiência do usuário mais imersiva e interativa. Ele permite que os desenvolvedores usem ferramentas conhecidas, como o HTML, JavaScript, Flash ou Adobe® Flex® software para implantar sua combinação exclusiva de aplicativos avançados de Internet no Windows, Macintosh ou Linux.

As empresas têm controle total da interface do usuário e podem projetar uma experiência do usuário para refletir e reforçar sua marca. Com suporte integrado para reprodução de conteúdo protegido com o SDK do Adobe Access, o Adobe AIR ajuda a criar cadeias de distribuição de conteúdo personalizadas e completas.

Para obter mais informações sobre o Adobe AIR, visite: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Aplicativos nativos iOS e Android {#native-ios-and-android-applications}

Aplicativos nativos iOS e Android Disponíveis somente para clientes da Adobe Primetime, o DRM 4.0 de Adobe Access e superior pode ser usado para proteger o vídeo consumido em aplicativos nativos (não Flashes) em dispositivos móveis. Para que um aplicativo consuma esse conteúdo protegido, ele deve ser implementado com o uso das bibliotecas de clientes do Adobe Primetime.

Para obter mais informações sobre o Adobe Primetime, visite: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)