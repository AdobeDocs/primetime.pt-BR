---
seo-title: Implantar Adobe Primetime DRM
title: Implantar Adobe Primetime DRM
uuid: c14c2792-d207-4f39-b856-610520bdaa28
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Implantar Adobe Primetime DRM {#configure-adobe-primetime-drm}

Uma vantagem importante para o Adobe Primetime DRM SDK é que você pode instalá-lo em qualquer servidor de aplicativos Java™ ou container de servlet, como Tomcat. Você também precisa do JDK™ 1.5 ou superior. Para obter mais informações sobre os requisitos de software, consulte Requisitos da plataforma SDK do Primetime DRM: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

As etapas de alto nível para implantar o Primetime DRM são:

1. Instale e configure o Primetime DRM SDK.
1. Obtenha certificados digitais do Adobe.
1. Crie um Servidor de Licenças usando o SDK ou implante o Primetime DRM Server para Protected Streaming.
1. Crie ferramentas de empacotamento de conteúdo e gerenciamento de políticas para empacotar conteúdo, use as ferramentas de preparação de conteúdo fornecidas ou licencie um dos empacotadores de HTTP Dynamic Streaming de Adobe.
1. Defina as regras de uso para o seu conteúdo e crie políticas de suporte a essas regras.
1. Empacote seu conteúdo usando as ferramentas de empacotamento e gerenciamento de políticas.
1. Desenvolva aplicativos de vídeo com os quais os consumidores possam visualização de seu conteúdo protegido usando o Flash Player ou Adobe AIR, ou use uma OVP (Online Video Platform) estabelecida que suporte o Primetime DRM.
1. Implante um arquivo SWF para uso com Flash Player em seu site ou poste o instalador da Adobe AIR para download.

Essas etapas são expandidas nas seções a seguir, com referências a outros documentos contendo informações adicionais.

## Implantação em um sistema operacional de 64 bits{#deploying-on-a-bit-operating-system}

Um sistema operacional de 64 bits, como a versão de 64 bits do RedHat ou do Windows, proporciona um desempenho muito melhor do que um sistema operacional de 32 bits.

## Instalar o Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

O Primetime DRM SDK é fornecido como um arquivo de arquivo Java (JAR). Para saber mais sobre como instalar o Primetime DRM, consulte Usar o Adobe Primetime DRM SDK para proteger conteúdo e diretrizes de implantação segura.

## Implementação de um License Server {#implement-a-license-server}

Usando o Adobe Primetime DRM SDK, é necessário criar um License Server. Quando o conteúdo é protegido usando o Primetime DRM, ele não pode ser exibido até que uma licença seja emitida ao consumidor pelo License Server. Se o licenciamento baseado em identidade for usado, a autenticação baseada em senha garante que somente os consumidores autorizados possam abrir e visualização conteúdo.

Ao implementar um License Server, você deve obter os certificados digitais necessários do Adobe. Consulte o documento de inscrição de certificado DRM Primetime para obter instruções detalhadas sobre como solicitar certificados.

Para saber mais sobre a implementação de um License Server e a obtenção de certificados digitais, consulte **Usando o Adobe Primetime DRM SDK para Proteção de Conteúdo.**

## Criar pacotes de conteúdo e ferramentas de gerenciamento de políticas{#create-content-packaging-and-policy-management-tools}

Usando o Adobe Primetime DRM SDK, é possível criar pacotes de conteúdo e ferramentas de gerenciamento de políticas. As APIs de gerenciamento de políticas permitem que os administradores criem, visualizações e atualizem políticas. As APIs de empacotamento incorporam a política ao arquivo de vídeo e criptografam o arquivo usando a chave de criptografia de conteúdo.

O SDK do DRM Primetime inclui uma implementação de referência ( [!DNL AdobePackager.jar]) que fornece exemplos de pacotes de conteúdo e ferramentas de gerenciamento de políticas ( [!DNL AdobePolicyManager.jar]).

Para saber mais sobre a criação de pacotes de conteúdo e ferramentas de gerenciamento de políticas, consulte **Usar o SDK do Adobe Primetime DRM para proteção de conteúdo.**

## Criar políticas e conteúdo do pacote {#create-policies-and-package-content}

Usando as regras de uso suportadas pelo SDK, você deve definir e criar políticas de suporte ao modelo de negócios de sua organização e, em seguida, disponibilizar seu conteúdo usando essas políticas. Depois que as políticas forem aplicadas ao conteúdo durante o empacotamento, você poderá manter o controle do conteúdo, independentemente de sua distribuição.

As políticas no Adobe Primetime DRM oferecem suporte a uma grande variedade de diferentes regras de uso, incluindo:

* Especificar o número de dias em que uma licença é válida quando um consumidor começa a assistir ao conteúdo.
* Permitindo o armazenamento em cache de licenças.
* Especificar os tempos de execução e as versões do cliente que podem acessar o conteúdo (por exemplo, os usuários devem ter um determinado aplicativo Adobe AIR ou uma versão específica do Flash Player).
* Exigir que os consumidores se autentiquem usando um nome de usuário e senha antes de exibir conteúdo protegido ou permitir acesso anônimo.

Para saber mais sobre como empacotar conteúdo, consulte *Protegendo Conteúdo*. Para saber mais sobre as regras de uso e os modelos de negócios compatíveis, consulte *Regras de uso*.

## Desenvolver aplicativos para reprodução de vídeo {#develop-applications-for-video-playback}

Para permitir que os consumidores acessem e visualizações de conteúdo, desenvolva um aplicativo de reprodução de vídeo usando o Flash Player ou o Adobe AIR. Depois de desenvolver um aplicativo de reprodução de vídeo, você deve implantá-lo nos consumidores. Se você estiver desenvolvendo um aplicativo usando o Flash Player, hospede-o no site de sua organização. Se você estiver desenvolvendo um aplicativo usando o Adobe® AIR®, publique o instalador do aplicativo AIR para que os consumidores possam baixar e instalar o aplicativo em seus computadores.

Para saber mais sobre o desenvolvimento de aplicativos personalizados de reprodução de vídeo para uso com o Adobe Primetime DRM, consulte o capítulo &quot;Trabalhando com vídeo&quot; no [Guia do desenvolvedor do ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), no [Centro de tecnologia de vídeo do Adobe](https://www.adobe.com/devnet/video/) e no Open Source Media Framework.