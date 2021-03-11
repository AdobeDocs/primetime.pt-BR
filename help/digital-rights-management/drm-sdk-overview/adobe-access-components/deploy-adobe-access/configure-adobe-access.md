---
title: Implantar Adobe Primetime DRM
description: Implantar Adobe Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Implantar Adobe Primetime DRM {#configure-adobe-primetime-drm}

Uma vantagem importante para o SDK do Adobe Primetime DRM é que você pode instalá-lo em qualquer servidor de aplicativos Java™ ou contêiner de servlet, como o Tomcat. Você também precisa do JDK™ 1.5 ou superior. Para obter mais informações sobre requisitos de software, consulte Requisitos da plataforma SDK de DRM do Primetime: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

As etapas de alto nível para implantar o Primetime DRM são:

1. Instale e configure o SDK de DRM do Primetime.
1. Obtenha certificados digitais do Adobe.
1. Crie um License Server usando o SDK ou implante o Primetime DRM Server for Protected Streaming.
1. Crie o empacotamento de conteúdo e as ferramentas de gerenciamento de políticas para empacotar conteúdo, use as ferramentas de preparação de conteúdo fornecidas ou licencie um dos pacotes de HTTP Dynamic Streaming de Adobe.
1. Defina as regras de uso para o seu conteúdo e crie políticas de suporte a essas regras.
1. Embale seu conteúdo usando as ferramentas de empacotamento e gerenciamento de políticas.
1. Desenvolva aplicativos de vídeo com os quais os consumidores possam visualizar seu conteúdo protegido usando o Flash Player ou Adobe AIR, ou use uma OVP (Online Video Platform) estabelecida que seja compatível com o Primetime DRM.
1. Implante um arquivo SWF para usar com o Flash Player no site ou poste o instalador do Adobe AIR para download.

Essas etapas são expandidas nas seções a seguir, com referências a outros documentos contendo informações adicionais.

## Implantação em um sistema operacional de 64 bits{#deploying-on-a-bit-operating-system}

Um sistema operacional de 64 bits, como a versão de 64 bits do RedHat ou do Windows, fornece desempenho muito melhor do que um sistema operacional de 32 bits.

## Instalar o SDK do Adobe Primetime DRM {#install-adobe-primetime-drm-sdk}

O SDK de DRM do Primetime é fornecido como um arquivo de arquivo Java (JAR). Para saber mais sobre a instalação do Primetime DRM, consulte Uso do Adobe Primetime DRM SDK para proteção de conteúdo e diretrizes de implantação segura.

## Implementar um Servidor de Licenças {#implement-a-license-server}

Com o Adobe Primetime DRM SDK, você deve criar um License Server. Quando o conteúdo é protegido por meio do DRM do Primetime, ele não pode ser visualizado até que uma licença seja emitida para o consumidor pelo License Server. Se o licenciamento com base na identidade for usado, a autenticação com senha garante que somente os consumidores autorizados possam abrir e visualizar o conteúdo.

Ao implementar um License Server, você deve obter os certificados digitais necessários do Adobe. Consulte o documento de Inscrição de Certificado DRM do Primetime para obter instruções detalhadas sobre a solicitação de certificados.

Para saber mais sobre como implementar um Servidor de licenças e obter certificados digitais, consulte **Usar o SDK de DRM do Adobe Primetime para proteger conteúdo.**

## Criar pacotes de conteúdo e ferramentas de gerenciamento de políticas{#create-content-packaging-and-policy-management-tools}

Com o Adobe Primetime DRM SDK, você pode criar pacotes de conteúdo e ferramentas de gerenciamento de políticas. As APIs de gerenciamento de políticas permitem que os administradores criem, visualizem detalhes e atualizem políticas. As APIs de empacotamento incorporam a política ao arquivo de vídeo e criptografam o arquivo usando a chave de criptografia de conteúdo.

O SDK de DRM do Primetime inclui uma implementação de referência ( [!DNL AdobePackager.jar]) que fornece exemplos de pacotes de conteúdo e ferramentas de gerenciamento de políticas ( [!DNL AdobePolicyManager.jar]).

Para saber mais sobre como criar pacotes de conteúdo e ferramentas de gerenciamento de políticas, consulte **Usar o SDK do Adobe Primetime DRM para proteção de conteúdo.**

## Criar políticas e conteúdo do pacote {#create-policies-and-package-content}

Usando as regras de uso compatíveis com o SDK, você deve definir e criar políticas de suporte ao modelo de negócios de sua organização e, em seguida, empacotar seu conteúdo usando essas políticas. Uma vez que as políticas sejam aplicadas ao conteúdo durante o empacotamento, você pode manter o controle do conteúdo independentemente de qual ele seja distribuído.

As políticas no DRM Adobe Primetime suportam uma grande variedade de regras de uso diferentes, incluindo:

* Especificação do número de dias em que uma licença é válida, assim que o consumidor começa a assistir ao conteúdo.
* Permitindo o armazenamento em cache de licenças.
* Especificar tempos de execução e versões do cliente que podem acessar conteúdo (por exemplo, os usuários devem ter um determinado aplicativo do Adobe AIR ou uma versão específica do Flash Player).
* Exigir que os consumidores se autentiquem usando um nome de usuário e senha antes de visualizar conteúdo protegido ou permitir acesso anônimo.

Para saber mais sobre conteúdo de pacote, consulte *Protegendo Conteúdo*. Para saber mais sobre as regras de uso e os modelos de negócios compatíveis, consulte *Regras de uso*.

## Desenvolver aplicativos para a reprodução de vídeo {#develop-applications-for-video-playback}

Para permitir que os consumidores acessem e visualizem conteúdo, desenvolva um aplicativo de reprodução de vídeo usando o Flash Player ou Adobe AIR. Depois de desenvolver um aplicativo de reprodução de vídeo, você deve implantá-lo nos consumidores. Se você estiver desenvolvendo um aplicativo usando o Flash Player, hospede-o no site de sua organização. Se você estiver desenvolvendo um aplicativo usando o Adobe® AIR®, publique o instalador do aplicativo AIR para que os consumidores possam baixar e instalar o aplicativo em seu computador.

Para saber mais sobre o desenvolvimento de aplicativos personalizados de reprodução de vídeo para uso com o Adobe Primetime DRM, consulte o capítulo &quot;Trabalhar com vídeo&quot; no [Guia do desenvolvedor do ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), no [Centro de tecnologia de vídeo Adobe](https://www.adobe.com/devnet/video/) e no Open Source Media Framework.