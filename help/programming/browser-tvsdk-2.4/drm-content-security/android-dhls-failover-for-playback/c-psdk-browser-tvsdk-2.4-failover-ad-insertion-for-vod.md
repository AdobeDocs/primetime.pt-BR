---
description: O processo de inserção de anúncio por vídeo sob demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK do navegador deve informar um servidor de rastreamento remoto sobre o progresso da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.
title: Inserção de publicidade e failover para VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# Inserção de publicidade e failover para VOD{#advertising-insertion-and-failover-for-vod}

O processo de inserção de anúncio por vídeo sob demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK do navegador deve informar um servidor de rastreamento remoto sobre o progresso da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.

## Fase de resolução de anúncios {#section_F562CD6D0EF04AA9A0A3C0176A4EC340}

O TVSDK do navegador entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK do navegador faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.

O TVSDK do navegador é compatível com os seguintes tipos de provedores de anúncios:

* Provedor de publicidade de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de tomada de decisão do Adobe Primetime

   O TVSDK do navegador envia uma solicitação, incluindo um conjunto de parâmetros de direcionamento e um número de identificação do ativo, para o servidor back-end de decisão do anúncio do Adobe Primetime. O Adobe Primetime ad decisioning responde com um documento SMIL (linguagem de integração de multimídia sincronizada) que contém as informações de anúncio necessárias.

   Uma das seguintes situações de failover pode ocorrer durante esta fase:

   * Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou um erro no lado do servidor, como um recurso não pode ser encontrado e assim por diante.
   * Os dados foram recuperados, mas o formato é inválido.

      Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.
   O TVSDK do navegador emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de inserção de anúncio {#section_88A0E4FA12394717A9D85689BD11D59F}

O TVSDK do navegador insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios estiver concluída, o TVSDK do navegador terá uma lista ordenada de recursos de anúncios que são agrupados em ad breaks. Cada ad break é posicionado na linha do tempo do conteúdo principal usando um valor de hora de início expresso em milissegundos (ms). Cada anúncio em um ad break tem uma propriedade duration que também é expressa em ms. Os anúncios em um ad break são encadeados um após o outro. Como resultado, a duração de um ad break é igual à soma das durações dos anúncios compostos individuais.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de tempo de início/duração do ad break, os segmentos de anúncio podem se sobrepor. A sobreposição ocorre quando a última parte de um ad break faz interseção com o início do primeiro anúncio no próximo ad break. Nessas situações, o TVSDK do navegador descarta o ad break posterior e continua o processo de inserção do anúncio com o próximo item na lista até que todas as quebras de anúncio sejam inseridas ou descartadas.

O TVSDK do navegador emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de reprodução de anúncio {#section_7B0073BE9A744C74929263182C1243FC}

O TVSDK do navegador baixa os segmentos de publicidade e os renderiza na tela do dispositivo.

Nesse momento, o TVSDK do navegador resolveu os anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As principais classes de erros a seguir podem ocorrer nesta fase:

* Erros ao conectar ao servidor host
* Erros ao baixar o arquivo manifest
* Erros ao baixar os segmentos de mídia

Para todas as três classes de erro, o TVSDK do navegador encaminha eventos acionados para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Eventos de notificação acionados quando todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Se ocorrerem erros ou não, o TVSDK do navegador notifica você quando um ad break é iniciado e quando ele é concluído. No entanto, se os segmentos não puderem ser baixados, pode haver lacunas na linha do tempo. Quando as lacunas são grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
