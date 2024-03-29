---
title: Implantar o Adobe Primetime DRM
description: Implantar o Adobe Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Implantar o Adobe Primetime DRM {#configure-adobe-primetime-drm}

Uma vantagem importante do SDK do Adobe Primetime DRM é que você pode instalá-lo em qualquer servidor de aplicativos Java™ ou contêiner de servlet, como Tomcat. Você também precisa do JDK™ 1.5 ou superior. Para obter mais informações sobre requisitos de software, consulte Requisitos da plataforma do SDK do DRM do Primetime: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

As etapas de alto nível para implantar o Primetime DRM são:

1. Instale e configure o SDK do DRM do Primetime.
1. Obtenha certificados digitais do Adobe.
1. Crie um License Server usando o SDK ou implante o Primetime DRM Server para transmissão protegida.
1. Crie pacotes de conteúdo e ferramentas de gerenciamento de políticas para empacotar conteúdo, use as ferramentas de preparação de conteúdo fornecidas ou licencie um dos empacotadores de Adobe HTTP Dynamic Streaming.
1. Defina regras de uso para o seu conteúdo e crie políticas para dar suporte a essas regras.
1. Crie pacotes de conteúdo usando as ferramentas de gerenciamento de pacotes e políticas.
1. Desenvolva aplicativos de vídeo com os quais os consumidores possam visualizar seu conteúdo protegido usando o Flash Player ou o Adobe AIR, ou use um OVP (Plataforma de vídeo online) estabelecido que ofereça suporte ao DRM do Primetime.
1. Implante um arquivo SWF para usar com o Flash Player em seu site ou publique o instalador do Adobe AIR para download.

Essas etapas são expandidas nas seções a seguir, com referências a outros documentos contendo informações adicionais.

## Implantação em um sistema operacional de 64 bits{#deploying-on-a-bit-operating-system}

Um sistema operacional de 64 bits, como a versão de 64 bits do RedHat ou do Windows, fornece um desempenho muito melhor do que um sistema operacional de 32 bits.

## Instalar o SDK do Adobe Primetime DRM {#install-adobe-primetime-drm-sdk}

O SDK do DRM do Primetime é fornecido como um arquivo Java (JAR). Para saber mais sobre como instalar o Primetime DRM, consulte Uso do SDK do Adobe Primetime DRM para proteção de conteúdo e diretrizes de implantação segura.

## Implementar um servidor de licenças {#implement-a-license-server}

Usando o SDK do Adobe Primetime DRM, você deve criar um License Server. Quando o conteúdo é protegido usando o Primetime DRM, ele não pode ser exibido até que uma licença seja emitida para o consumidor pelo License Server. Se o licenciamento baseado em identidade for usado, a autenticação baseada em senha garante que somente os consumidores autorizados possam abrir e visualizar o conteúdo.

Ao implementar um License Server, você deve obter os certificados digitais necessários do Adobe. Consulte o documento Registro de certificado DRM do Primetime para obter instruções detalhadas sobre como solicitar certificados.

Para saber mais sobre como implementar um License Server e obter certificados digitais, consulte **Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo.**

## Criar pacotes de conteúdo e ferramentas de gerenciamento de políticas{#create-content-packaging-and-policy-management-tools}

Usando o SDK do Adobe Primetime DRM, você pode criar pacotes de conteúdo e ferramentas de gerenciamento de políticas. As APIs de gerenciamento de políticas permitem que os administradores criem, exibam detalhes e atualizem políticas. As APIs de empacotamento incorporam a política ao arquivo de vídeo e criptografam o arquivo usando a chave de criptografia de conteúdo.

O SDK do DRM do Primetime inclui uma implementação de referência ( [!DNL AdobePackager.jar]) que fornece exemplos de pacotes de conteúdo e ferramentas de gerenciamento de políticas ( [!DNL AdobePolicyManager.jar]).

Para saber mais sobre como criar pacotes de conteúdo e ferramentas de gerenciamento de políticas, consulte **Uso do SDK do Adobe Primetime DRM para proteção de conteúdo.**

## Criar políticas e conteúdo do pacote {#create-policies-and-package-content}

Usando as regras de uso compatíveis com o SDK, você deve definir e criar políticas para dar suporte ao modelo de negócios da organização e, em seguida, criar pacotes de conteúdo usando essas políticas. Depois que as políticas forem aplicadas ao conteúdo durante o empacotamento, você poderá manter o controle do conteúdo, independentemente da abrangência da sua distribuição.

As políticas no Adobe Primetime DRM são compatíveis com uma grande variedade de regras de uso, incluindo:

* Especificar o número de dias que uma licença é válida assim que um consumidor começa a assistir ao conteúdo.
* Permitindo o armazenamento em cache de licenças.
* Especificação dos tempos de execução do cliente e das versões que podem acessar o conteúdo (por exemplo, os usuários devem ter determinado aplicativo Adobe AIR ou uma versão específica do Flash Player).
* Exigir que os consumidores se autentiquem usando um nome de usuário e senha antes de visualizar o conteúdo protegido ou permitir o acesso anônimo.

Para saber mais sobre o conteúdo de pacotes, consulte *Protegendo conteúdo*. Para saber mais sobre as regras de uso e os modelos de negócios aceitos, consulte *Regras de uso*.

## Desenvolver aplicativos para reprodução de vídeo {#develop-applications-for-video-playback}

Para permitir que os consumidores acessem e visualizem conteúdo, desenvolva um aplicativo de reprodução de vídeo usando o Flash Player ou o Adobe AIR. Depois de desenvolver um aplicativo de reprodução de vídeo, você deve implantá-lo nos consumidores. Se você estiver desenvolvendo um aplicativo usando o Flash Player, hospede-o no site da empresa. Se você estiver desenvolvendo um aplicativo usando o Adobe® AIR®, publique o instalador do aplicativo do AIR para que os consumidores possam baixar e instalar o aplicativo em seus computadores.

Para saber mais sobre como desenvolver aplicativos de reprodução de vídeo personalizados para uso com o Adobe Primetime DRM, consulte o capítulo &quot;Trabalho com vídeo&quot; em [Guia do desenvolvedor do ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), o [Centro de tecnologia de vídeo Adobe](https://www.adobe.com/devnet/video/), e o Open Source Media Framework.
