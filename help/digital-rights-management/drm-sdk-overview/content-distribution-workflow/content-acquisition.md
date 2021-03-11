---
description: 'Quando um consumidor adquire um arquivo de conteúdo protegido de um site ou CDN, o consumidor também deve adquirir uma licença que contenha uma chave para descriptografar o vídeo antes que ele possa ser reproduzido. As etapas a seguir ilustram um fluxo de trabalho comum de como o conteúdo protegido é acessado por um computador que executa o Flash Player ou o Adobe AIR '
title: Aquisição de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Aquisição de conteúdo{#content-acquisition}

Quando um consumidor adquire um arquivo de conteúdo protegido de um site ou CDN, o consumidor também deve adquirir uma licença que contenha uma chave para descriptografar o vídeo antes que ele possa ser reproduzido. As etapas a seguir ilustram um fluxo de trabalho comum de como o conteúdo protegido é acessado por um computador que executa o Flash Player ou o Adobe AIR:

1. O consumidor visita o site da varejista e seleciona um vídeo para assistir. O consumidor tenta baixar ou fazer o stream do vídeo protegido para o computador usando o Flash Player ou um aplicativo Adobe AIR.

   Se esta for a primeira vez que o consumidor tenta acessar o conteúdo protegido usando este computador específico, o tempo de execução do Flash Player ou Adobe AIR deve primeiro ser individualizado, conforme descrito na Etapa 2. Se o cliente de tempo de execução já tiver sido individualizado, o processo de aquisição de uma licença ocorrerá conforme descrito na Etapa 3.

1. O cliente de tempo de execução do Flash Player ou Adobe AIR adquire um certificado digital exclusivo (chamado de *machine certificate*) de um servidor hospedado no Adobe.

   Esse processo de atribuição de um certificado exclusivo é chamado de *individualização*. A individualização identifica exclusivamente o computador e o tempo de execução do Flash Player ou Adobe AIR usado para reproduzir o conteúdo.

   O processo de individualização permite que as licenças baixadas sejam vinculadas a um computador específico no qual o cliente está instalado. A cada computador é dada uma credencial de máquina exclusiva (chave privada da máquina e certificado de máquina). Se um cliente específico for comprometido, ele poderá ser revogado e impedido de adquirir licenças para novos conteúdos.

1. O cliente analisa o conteúdo protegido à medida que ele começa a baixar ou fazer stream no computador do consumidor e extrai o URL do License Server do varejista dos metadados DRM do Primetime incorporados ao arquivo.

   Os metadados de DRM do Primetime geralmente são separados do conteúdo, como incorporado em um arquivo de manifesto de acompanhamento ou como um blob binário, mas também pode ser incorporado no arquivo de conteúdo. O cliente entra em contato com o License Server no URL especificado e adquire uma licença (conforme descrito abaixo na Etapa 4).
1. O cliente adquire uma licença do License Server do varejista.

   Durante a aquisição de licença, o cliente envia informações que identificam o conteúdo solicitado (os *metadados de DRM do Primetime*) e o certificado da máquina (identificando o computador do consumidor) para o License Server do varejista. A solicitação de licença enviada ao servidor é criptografada usando a chave pública Transport, que também está incluída nos metadados DRM do Primetime.

   O License Server — que pode ser integrado à infraestrutura de faturamento e autenticação do varejista — pode executar uma verificação de regras de negócios para verificar se o usuário está autorizado a exibir o conteúdo solicitado. Se as regras comerciais o permitirem, o License Server emite uma licença contendo a chave de criptografia de conteúdo para descriptografar o conteúdo e as regras de uso associadas à conta desse usuário. Para processar uma solicitação de licença, o License Server descriptografa a solicitação usando sua chave privada Transport. O CEK nos metadados é descriptografado usando a chave privada do License Server e criptografado novamente para vincular a licença ao dispositivo que faz a solicitação. A licença é assinada usando a chave privada do servidor de licenças. A resposta da licença é assinada usando a chave privada Transport e criptografada antes de ser retornada ao cliente.

   Se permitido pela licença, o cliente armazena a licença para habilitar *offline access* para a licença. O armazenamento em cache de licenças permite que o consumidor visualize conteúdo protegido sem adquirir novamente uma licença sempre que quiser visualizar o conteúdo.

1. Quando o cliente do Flash Player ou do Adobe AIR Runtime tiver uma licença, o cliente extrairá o CEK da licença e o consumidor poderá visualizar o conteúdo que está autorizado a acessar.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   O exemplo anterior mostra apenas um workflow possível. Como alternativa, você pode usar um fluxo de trabalho com um download pró-ativo do conteúdo, onde a aquisição da licença acontece muito mais tarde. Outra opção é implementar um fluxo de trabalho de pré-pedido no qual a aquisição de licença ocorre antes do conteúdo ser acessado.

