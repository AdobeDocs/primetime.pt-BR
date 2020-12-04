---
description: 'Quando um consumidor adquire um arquivo de conteúdo protegido de um site ou CDN, o consumidor também deve adquirir uma licença que contenha uma chave para descriptografar o vídeo antes que ele possa ser reproduzido. As etapas a seguir ilustram um fluxo de trabalho comum para ver como o conteúdo protegido é acessado por um computador que executa o Flash Player ou o Adobe AIR '
seo-description: 'Quando um consumidor adquire um arquivo de conteúdo protegido de um site ou CDN, o consumidor também deve adquirir uma licença que contenha uma chave para descriptografar o vídeo antes que ele possa ser reproduzido. As etapas a seguir ilustram um fluxo de trabalho comum para ver como o conteúdo protegido é acessado por um computador que executa o Flash Player ou o Adobe AIR '
seo-title: Aquisição de conteúdo
title: Aquisição de conteúdo
uuid: 80253746-bc31-43f0-b28b-7a1aa7fe34a7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# Aquisição de conteúdo{#content-acquisition}

Quando um consumidor adquire um arquivo de conteúdo protegido de um site ou CDN, o consumidor também deve adquirir uma licença que contenha uma chave para descriptografar o vídeo antes que ele possa ser reproduzido. As etapas a seguir ilustram um fluxo de trabalho comum para saber como o conteúdo protegido é acessado por um computador que executa o Flash Player ou o Adobe AIR:

1. O consumidor visita o site do varejista e seleciona um vídeo para assistir. O consumidor tenta baixar ou transmitir o vídeo protegido para seu computador usando um Flash Player ou aplicativo Adobe AIR.

   Se esta for a primeira vez que o consumidor tenta acessar o conteúdo protegido usando este computador específico, o Flash Player ou o tempo de execução do Adobe AIR deve ser individualizado, conforme descrito na Etapa 2. Se o cliente de tempo de execução já tiver sido individualizado, o processo de aquisição de uma licença ocorrerá conforme descrito na Etapa 3.

1. O cliente de tempo de execução do Flash Player ou Adobe AIR adquire um certificado digital exclusivo (chamado de *certificado de máquina*) de um servidor hospedado no Adobe.

   Esse processo de atribuição de um certificado exclusivo é chamado *individualização*. A individualização identifica exclusivamente o computador e o Flash Player ou o tempo de execução do Adobe AIR usados para reproduzir o conteúdo.

   O processo de individualização permite que as licenças baixadas sejam vinculadas a um computador específico no qual o cliente está instalado. A cada computador é dada uma credencial de máquina exclusiva (chave privada da máquina e certificado da máquina). Se um cliente específico for comprometido, ele poderá ser revogado e impedido de adquirir licenças para novo conteúdo.

1. O cliente analisa o conteúdo protegido à medida que ele começa a baixar ou transmitir para o computador do consumidor e extrai o URL do servidor de licença do varejista dos metadados do DRM do Primetime incorporados ao arquivo.

   Os metadados DRM do Primetime geralmente são separados do conteúdo, como incorporados em um arquivo manifest acompanhante ou como um blob binário, mas também podem ser incorporados no arquivo de conteúdo. O cliente entra em contato com o License Server no URL especificado e adquire uma licença (conforme descrito abaixo na Etapa 4).
1. O cliente adquire uma licença do License Server do varejista.

   Durante a aquisição da licença, o cliente envia informações que identificam o conteúdo solicitado (os *metadados do Primetime DRM*) e o certificado da máquina (identificando o computador do consumidor) para o License Server do varejista. A solicitação de licença enviada para o servidor é criptografada usando a chave pública Transport, que também está incluída nos metadados do Primetime DRM.

   O License Server — que podem ser integrados na infraestrutura de faturação e autenticação do retalhista. pode executar uma verificação de regras comerciais para verificar se o usuário está autorizado a visualização do conteúdo solicitado. Se as regras de negócios o permitirem, o License Server emite uma licença contendo a chave de criptografia de conteúdo para descriptografar o conteúdo e as regras de uso associadas à conta desse usuário. Para processar uma solicitação de licença, o License Server descriptografa a solicitação usando sua chave privada de Transporte. O CEK nos metadados é descriptografado usando a chave privada do License Server e criptografado novamente para vincular a licença ao dispositivo que faz a solicitação. A licença é assinada usando a chave privada do servidor de licença. A resposta da licença é assinada usando a chave privada de Transporte e criptografada antes de ser retornada ao cliente.

   Se permitido pela licença, o cliente armazena a licença para habilitar *acesso offline* à licença. O armazenamento em cache de licenças permite que o consumidor faça visualização de conteúdo protegido sem precisar readquirir uma licença sempre que quiser fazer visualização de conteúdo.

1. Depois que o cliente de tempo de execução do Flash Player ou Adobe AIR tiver uma licença, o cliente extrai o CEK da licença e o consumidor poderá visualização o conteúdo ao qual está autorizado acesso.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   O exemplo anterior mostra apenas um fluxo de trabalho possível. Como alternativa, você pode usar um fluxo de trabalho com um download pró-ativo de conteúdo no qual a aquisição da licença acontece muito mais tarde. Outra opção é implementar um fluxo de trabalho pré-pedido no qual a aquisição da licença ocorre antes do conteúdo ser acessado.

