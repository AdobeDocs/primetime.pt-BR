---
description: Os principais componentes do Adobe Access consistem em um SDK Java e nos ambientes de tempo de execução de cliente Flash Player e Adobe AIR.
title: SDK do Java, Flash Player e cliente Adobe AIR
exl-id: 2df4da13-8df9-442b-8638-317c41d62fbe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Componentes de acesso ao Adobe{#adobe-access-components}

Os principais componentes do Adobe Access consistem em um SDK Java e nos ambientes de tempo de execução de cliente Flash Player e Adobe AIR.

Para obter mais informações sobre como configurar o SDK, consulte Configuração do SDK em *Utilização do SDK do Adobe Access para proteção de conteúdo.*

O SDK de acesso do Adobe permite desenvolver uma solução de gerenciamento de direitos digitais que se integra à infraestrutura comercial existente da sua organização, como gerenciamento de conteúdo, cobrança e sistemas de controle de acesso do usuário. O Flash Player e o Adobe AIR permitem criar e implantar facilmente aplicativos através dos quais os consumidores podem acessar e visualizar grandes bibliotecas de conteúdo digital.

## SDK de acesso do Adobe {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

O Acesso ao Adobe é fornecido como um SDK Java que fornece os blocos de construção a partir dos quais você pode criar uma implementação de servidor. Usando o SDK, você pode criar uma solução de acesso ao Adobe adequada ao modelo de negócios de sua organização.

As APIs Java fornecidas no SDK estão descritas nas subseções a seguir.

## APIs Java para gerenciar domínios de grupos de dispositivos {#java-apis-for-managing-device-group-domains}

Essas APIs são usadas para permitir que o servidor manipule solicitações de clientes para ingressar e sair de domínios de grupos de dispositivos.

Um domínio de grupo de dispositivos é uma coleção lógica de dispositivos que podem compartilhar licenças entre si. Para que isso aconteça, cada dispositivo deve primeiro ingressar/registrar no mesmo domínio. O SDK de acesso do Adobe, em execução em um servidor, deve lidar com as solicitações de associação (registro) do domínio do dispositivo, bem como com as solicitações de licença (cancelamento de registro) do domínio do dispositivo. Os dispositivos que não ingressaram em nenhum domínio receberão licenças vinculadas a esse dispositivo, que não podem ser compartilhadas com nenhum outro dispositivo.

## APIs Java para proteção de conteúdo {#java-apis-for-protecting-content}

Essas APIs são usadas para definir direitos e preparar conteúdo para distribuição. As APIs de proteção de conteúdo são:

* Gerenciamento de políticas

   A API de gerenciamento de política é usada para criar e modificar políticas a serem aplicadas ao conteúdo. As políticas podem ser criadas ou atualizadas, incluindo a obtenção/configuração de todas as regras de uso e a permissão de parâmetros adicionais em um namespace personalizado.

* Empacotamento de conteúdo

   A API de pacote de conteúdo é usada para criptografar o conteúdo e recuperar metadados do conteúdo do pacote.

## APIs Java para emissão de licenças {#java-apis-for-issuing-licenses}

Essas APIs são usadas quando um cliente solicita uma licença do servidor. O SDK é compatível com as seguintes solicitações do cliente:

* Autenticação

   A API de autenticação pode ser usada para lidar com solicitações de autenticação e gerar tokens de autenticação.

* Geração e aquisição de licença

   A API de geração e aquisição de licença é usada para gerar uma licença para o usuário.

* Suporte para clientes e conteúdo do Adobe AIR versão 1.5

   Para fins de compatibilidade com versões anteriores, o SDK tem APIs para lidar com solicitações de aplicativos do AIR criadas para uso com clientes AIR versão 1.5 e anteriores e conteúdo protegido.

## Implementação de referência {#reference-implementation}

O SDK inclui uma implementação de referência, uma implantação de acesso Adobe simples que demonstra como usar as APIs do Java. A implementação de referência fornece um License Server, um empacotador de pastas monitoradas, um aplicativo do Adobe Access Manager AIR e ferramentas de linha de comando para empacotamento de conteúdo e gerenciamento de políticas com base nas APIs Java. Para saber mais sobre a implementação da referência de Acesso ao Adobe, consulte *Protegendo conteúdo*.

## Adobe Access Server para transmissão protegida {#adobe-access-server-for-protected-streaming}

Para casos de uso de transmissão em que o conteúdo é protegido com o Adobe Access, como para Adobe HTTP Dynamic Streaming, o software também inclui o Adobe Access Server para transmissão protegida. Essa solução pode ser facilmente implantada em um container de servlet, como o Tomcat, e pode alcançar um alto nível de escalabilidade e desempenho para atender às maiores necessidades de distribuição de conteúdo.

## Flash Player Adobe {#adobe-flash-player}

O Flash Player é um plug-in e um tempo de execução leves de navegador que proporcionam experiências consistentes e envolventes ao usuário, reprodução impressionante de áudio/vídeo e alcance difundido. O Flash Player fornece reprodução de alta qualidade de conteúdo de vídeo transmitido ou baixado. Para editores de conteúdo, o Flash Player fornece os meios de personalizar as telas de reprodução que envolvem o conteúdo, permitindo experiências de marca mais profundas e monetização por meio da publicidade usando banners e sobreposições. Para os consumidores, o Flash Player apresenta uma maneira intuitiva e visualmente atraente de visualizar o conteúdo de vídeo.

Para obter mais informações sobre o Flash Player, visite: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

O Adobe AIR é um tempo de execução de vários sistemas operacionais que permite que os produtores de conteúdo estendam seus investimentos existentes na Web para o desktop, criando aplicativos multimídia personalizados. Baseado em tecnologias comprovadas e abertas, ele oferece uma maneira confiável e simplificada para as empresas desenvolverem e implantarem aplicativos personalizados que podem ser confiáveis para fornecer uma experiência do usuário mais segura e agradável. O Adobe AIR permite que as empresas integrem facilmente mídia avançada para criar uma experiência do usuário mais imersiva e interativa. Ele permite que os desenvolvedores usem ferramentas familiares, como o software HTML, JavaScript, Flash ou Adobe® Flex®, para implantar sua combinação exclusiva de aplicativos avançados de Internet no Windows, Macintosh ou Linux.

As empresas têm controle total da interface do usuário e podem projetar uma experiência do usuário para refletir e reforçar sua marca. Com suporte integrado para reprodução de conteúdo protegido com o SDK de acesso do Adobe, o Adobe AIR ajuda a criar cadeias de distribuição de conteúdo personalizadas e completas.

Para obter mais informações sobre o Adobe AIR, visite: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Aplicativos nativos iOS e Android {#native-ios-and-android-applications}

Aplicativos nativos iOS e Android Disponíveis apenas para clientes do Adobe Primetime, o Adobe Access DRM 4.0 e superior pode ser usado para proteger o vídeo consumido em aplicativos nativos (não Flashes) em dispositivos móveis. Para que um aplicativo consuma esse conteúdo protegido, ele deve ser implementado usando as bibliotecas de clientes do Adobe Primetime.

Para obter mais informações sobre o Adobe Primetime, visite: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
