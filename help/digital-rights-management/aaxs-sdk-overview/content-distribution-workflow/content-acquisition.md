---
title: Aquisição de conteúdo
description: Aquisição de conteúdo
copied-description: true
exl-id: 661bc6a1-34b6-4e0d-afbd-76f701728297
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Aquisição de conteúdo {#content-acquisition}

Quando um consumidor adquire um arquivo de conteúdo protegido de um site ou CDN, o consumidor também deve adquirir uma licença que contenha uma chave para descriptografar o vídeo antes que ele possa ser reproduzido. As etapas a seguir ilustram um fluxo de trabalho comum para como o conteúdo protegido é acessado por um computador que executa o Flash Player ou o Adobe AIR:

1. O consumidor visita o site do varejista e seleciona um vídeo para assistir. O consumidor tenta baixar ou transmitir o vídeo protegido para o computador usando o Flash Player ou um aplicativo do Adobe AIR.

   Se esta for a primeira vez que o consumidor tenta acessar conteúdo protegido usando este computador específico, o tempo de execução do Flash Player ou do Adobe AIR deve primeiro ser individualizado, conforme descrito na Etapa 2. Se o cliente de tempo de execução já tiver sido individualizado, o processo de aquisição de uma licença ocorrerá conforme descrito na Etapa 3.

1. O cliente de tempo de execução do Flash Player ou Adobe AIR adquire um certificado digital exclusivo (chamado de *certificado de máquina*) de um servidor hospedado em Adobe.

   Esse processo de atribuição de um certificado exclusivo é chamado de *individualização*. A personalização identifica exclusivamente o computador e o tempo de execução do Flash Player ou Adobe AIR usado para reproduzir conteúdo.

   O processo de individualização permite que as licenças baixadas sejam vinculadas a um computador específico no qual o cliente está instalado. Cada computador recebe uma credencial de máquina exclusiva (chave privada da máquina e certificado da máquina). Se um cliente específico for comprometido, ele poderá ser revogado e impedido de adquirir licenças para novo conteúdo.

1. O cliente analisa o conteúdo protegido à medida que ele começa a baixar ou transmitir para o computador do consumidor e extrai o URL do License Server do varejista dos metadados de DRM incorporados ao arquivo.

   Normalmente, os metadados de DRM são separados do conteúdo, como incorporados em um arquivo de manifesto que os acompanha ou como um blob binário, mas também podem ser incorporados ao arquivo de conteúdo. O cliente entra em contato com o License Server no URL especificado e adquire uma licença (conforme descrito abaixo na Etapa 4).
1. O cliente adquire uma licença do License Server do varejista.

   Durante a aquisição da licença, o cliente envia informações que identificam o conteúdo solicitado (o *Metadados de DRM*) e o certificado da máquina (identificando o computador do consumidor) para o License Server do varejista. A solicitação de licença enviada ao servidor é criptografada usando a chave pública Transport, que também está incluída nos metadados DRM.

   O License Server — que pode estar integrado à infraestrutura de faturamento e autenticação do varejista — pode executar uma verificação de regras de negócios para verificar se o usuário está autorizado a exibir o conteúdo solicitado. Se as regras de negócios permitirem, o License Server emitirá uma licença contendo a chave de criptografia de conteúdo para descriptografar o conteúdo e as regras de uso associadas à conta desse usuário. Para processar uma solicitação de licença, o License Server descriptografa a solicitação usando sua chave privada de transporte. O CEK nos metadados é descriptografado usando a chave privada do License Server e criptografado novamente para vincular a licença ao dispositivo que faz a solicitação. A licença é assinada usando a chave privada do servidor de licenças. A resposta da licença é assinada usando a chave privada Transport e criptografada antes de ser retornada ao cliente.

   Se permitido pela licença, o cliente armazena a licença para habilitar *acesso off-line* à licença. O armazenamento em cache de licenças permite que o consumidor visualize conteúdo protegido sem readquirir uma licença sempre que quiser visualizar conteúdo.

1. Depois que o cliente de tempo de execução do Flash Player ou do Adobe AIR tiver uma licença, o cliente extrairá o CEK da licença e o consumidor poderá exibir o conteúdo ao qual está autorizado a acessar.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   O exemplo anterior mostra apenas um fluxo de trabalho possível. Como alternativa, você pode usar um fluxo de trabalho com um download pró-ativo de conteúdo no qual a aquisição da licença acontece muito mais tarde. Outra opção é implementar um workflow de pré-pedido em que a aquisição da licença ocorre antes que o conteúdo seja acessado.
