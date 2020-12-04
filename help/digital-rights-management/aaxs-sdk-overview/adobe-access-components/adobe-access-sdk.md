---
description: Os principais componentes do Adobe Access consistem em um Java SDK e os ambientes de tempo de execução do cliente do Flash Player e do Adobe AIR.
seo-description: Os principais componentes do Adobe Access consistem em um Java SDK e os ambientes de tempo de execução do cliente do Flash Player e do Adobe AIR.
seo-title: Java SDK, Flash Player e cliente Adobe AIR
title: Java SDK, Flash Player e cliente Adobe AIR
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Componentes do Adobe Access{#adobe-access-components}

Os principais componentes do Adobe Access consistem em um Java SDK e os ambientes de tempo de execução do cliente do Flash Player e do Adobe AIR.

Para obter mais informações sobre como configurar o SDK, consulte Configuração do SDK em *Usando o SDK de Acesso ao Adobe para Proteção de Conteúdo.*

O SDK de acesso ao Adobe permite desenvolver uma solução de gerenciamento de direitos digitais que se integra à infraestrutura comercial existente da sua organização, como sistemas de gestão de conteúdo, faturamento e controle de acesso do usuário. O Flash Player e o Adobe AIR permitem que você crie e implante facilmente aplicativos através dos quais os consumidores possam acessar e visualização grandes bibliotecas de conteúdo digital.

## SDK de acesso ao Adobe {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

O Acesso ao Adobe é disponibilizado como um SDK Java que fornece os blocos componentes a partir dos quais você pode criar uma implementação do servidor. Usando o SDK, você pode criar uma solução de Adobe Access adequada ao modelo de negócios de sua organização.

As APIs Java fornecidas no SDK são descritas nas subseções a seguir.

## APIs Java para gerenciar domínios de grupos de dispositivos {#java-apis-for-managing-device-group-domains}

Essas APIs são usadas para permitir que o servidor manipule solicitações de clientes para ingressar e sair de domínios de grupos de dispositivos.

Um domínio de grupo de dispositivos é uma coleção lógica de dispositivos que podem compartilhar licenças entre si. Para que isso ocorra, cada dispositivo deve primeiro se conectar/registrar no mesmo domínio. O SDK de acesso ao Adobe, em execução em um servidor, deve processar as solicitações de ingresso (registro) do domínio do dispositivo, bem como as solicitações de licença do domínio do dispositivo (cancelamento de registro). Os dispositivos que não estão associados a nenhum domínio receberão licenças que estão vinculadas a esse dispositivo, que não podem ser compartilhadas com nenhum outro dispositivo.

## APIs Java para proteção de conteúdo {#java-apis-for-protecting-content}

Essas APIs são usadas para definir direitos e preparar conteúdo para distribuição. As APIs de proteção de conteúdo são:

* Gerenciamento de políticas

   A API de gerenciamento de políticas é usada para criar e modificar políticas a serem aplicadas ao conteúdo. As políticas podem ser criadas ou atualizadas, incluindo obter/definir todas as regras de uso e permitir parâmetros adicionais em uma namespace personalizada.

* Embalagem do conteúdo

   A API de empacotamento de conteúdo é usada para criptografar conteúdo e recuperar metadados do conteúdo empacotado.

## APIs Java para a emissão de licenças {#java-apis-for-issuing-licenses}

Essas APIs são usadas quando um cliente solicita uma licença do servidor. O SDK oferece suporte às seguintes solicitações do cliente:

* Autenticação

   A API de autenticação pode ser usada para manipular solicitações de autenticação e gerar tokens de autenticação.

* Geração e aquisição de licenças

   A API de geração e aquisição de licença é usada para gerar uma licença para o usuário.

* Suporte para clientes e conteúdo da versão 1.5 do Adobe AIR

   Para fins de compatibilidade com versões anteriores, o SDK tem APIs para lidar com solicitações de aplicativos AIR criados para uso com clientes AIR versão 1.5 e anteriores e conteúdo protegido.

## Implementação de referência {#reference-implementation}

O SDK inclui uma implementação de referência, uma implantação simples de acesso a Adobe que demonstra como usar as APIs Java. A implementação de referência fornece um License Server, Watched Folder Packager, um aplicativo AIR do Adobe Access Manager e ferramentas de linha de comando para o empacotamento de conteúdo e gerenciamento de políticas com base nas APIs do Java. Para saber mais sobre a implementação de referência do Acesso ao Adobe, consulte *Protegendo Conteúdo*.

## Adobe Access Server for Protected Streaming {#adobe-access-server-for-protected-streaming}

Para casos de uso de streaming em que o conteúdo é protegido com Adobe Access, como para Adobe HTTP Dynamic Streaming, o software também inclui Adobe Access Server para Protected Streaming. Essa solução pode ser facilmente implantada em um container de servlet, como o Tomcat, e pode atingir um alto nível de escalabilidade e desempenho para atender às maiores necessidades de distribuição de conteúdo.

## Flash Player Adobe {#adobe-flash-player}

O Flash Player é um leve plug-in e tempo de execução do navegador que oferece experiências consistentes e envolventes para o usuário, uma incrível reprodução de áudio/vídeo e um alcance abrangente. O Flash Player oferece reprodução de alta qualidade de conteúdo de vídeo transmitido ou baixado. Para os editores de conteúdo, o Flash Player fornece os meios de personalizar as telas de reprodução em torno do conteúdo, permitindo experiências de marca e monetização mais profundas por meio de anúncios usando banners e sobreposições. Para os consumidores, o Flash Player apresenta uma maneira intuitiva e visualmente atraente para o conteúdo de vídeo da visualização.

Para obter mais informações sobre o Flash Player, visite: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

A Adobe AIR é um tempo de execução entre sistemas operacionais que permite que os produtores de conteúdo estendam seus investimentos existentes na Web para o desktop ao projetar aplicativos multimídia personalizados. Construído com tecnologias comprovadas e abertas, ele oferece uma maneira confiável e simplificada para as empresas desenvolverem e implantarem aplicativos personalizados que podem ser confiáveis para oferecer uma experiência do usuário mais segura e agradável. A Adobe AIR permite que as empresas integrem facilmente mídias avançadas para criar uma experiência de usuário mais imersiva e interativa. Ele permite que os desenvolvedores usem ferramentas familiares, como HTML, JavaScript, Flash ou software de Flex®®, para implantar sua combinação exclusiva de aplicativos avançados de Internet no Windows, Macintosh ou Linux.

As empresas têm controle total da interface do usuário, e podem projetar uma experiência do usuário para refletir e reforçar sua marca. Com suporte integrado para reprodução de conteúdo protegido com SDK de acesso a Adobe, a Adobe AIR ajuda a criar cadeias de distribuição de conteúdo personalizadas e completas.

Para obter mais informações sobre o Adobe AIR, visite: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Aplicativos nativos iOS e Android {#native-ios-and-android-applications}

Aplicativos nativos iOS e Android Disponíveis somente para clientes Adobe Primetime, o Adobe Access DRM 4.0 e superior pode ser usado para proteger vídeos consumidos em aplicativos nativos (não Flashes) em dispositivos móveis. Para que um aplicativo consuma esse conteúdo protegido, ele deve ser implementado usando as bibliotecas do Adobe Primetime Client.

Para obter mais informações sobre o Adobe Primetime, visite: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)