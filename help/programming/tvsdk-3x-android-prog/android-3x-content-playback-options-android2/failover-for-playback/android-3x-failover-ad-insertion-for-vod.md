---
description: O processo de inserção de anúncios de vídeo sob demanda (VOD) consiste nas fases de resolução, inserção e reprodução de anúncios. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o progresso da reprodução de cada anúncio. Quando surgirem situações inesperadas, o TVSDK tomará as medidas apropriadas.
title: Inserção de publicidade e failover para VOD
exl-id: 0f5929eb-b6cf-4454-904a-2d4637177b68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Inserção de publicidade e failover para VOD {#advertising-insertion-and-failover-for-vod}

O processo de inserção de anúncios de vídeo sob demanda (VOD) consiste nas fases de resolução, inserção e reprodução de anúncios. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o progresso da reprodução de cada anúncio. Quando surgirem situações inesperadas, o TVSDK tomará as medidas apropriadas.

## Fase de resolução de anúncios {#section_5DD3A7DA79E946298BFF829A60202E1C}

O TVSDK entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.

O TVSDK é compatível com os seguintes tipos de provedores de anúncios:

* Provedor de anúncio de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão de anúncio do Primetime

   O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de direcionamento e um número de identificação de ativo, para o servidor de back-end do Primetime e da decisão. O Primetime ad Decisioning responde com um documento SMIL (Linguagem de integração de multimídia sincronizada) que contém as informações de anúncio necessárias.
* Provedor de marcadores de anúncios personalizados

   Trata a situação em que os anúncios são gravados no fluxo, a partir do lado do servidor. O TVSDK não executa a inserção real do anúncio, mas precisa acompanhar os anúncios inseridos no lado do servidor. Esse provedor define os marcadores de anúncios que o TVSDK usa para executar o rastreamento de anúncios.

Uma das seguintes situações de failover pode ocorrer durante essa fase:

* Os dados não podem ser recuperados devido, por exemplo, à falta de conectividade ou a um erro no lado do servidor, como a não localização de um recurso, e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

   Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de inserção do anúncio {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios for concluída, o TVSDK terá uma lista ordenada de recursos de anúncios agrupados em ad breaks. Cada ad break é posicionado na linha do tempo do conteúdo principal usando um valor de hora de início expresso em milissegundos (ms). Cada anúncio em um ad break tem uma propriedade de duração que também é expressa em ms. Os anúncios em um ad break são encadeados e, como resultado, a duração de um ad break é igual à soma das durações dos anúncios que compõem individualmente.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de hora de início/duração do ad break, os segmentos de anúncios podem se sobrepor. Essa sobreposição ocorre quando a última parte de um ad break intercepta o início do primeiro anúncio no próximo ad break. Nessas situações, o TVSDK descarta o ad break posterior e continua o processo de inserção de anúncios com o próximo item na lista até que todos os ad breaks sejam inseridos ou descartados.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de reprodução do anúncio {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

O TVSDK baixa os segmentos de anúncios e os renderiza na tela do dispositivo.

Agora, o TVSDK resolveu os anúncios, posicionou os anúncios na linha do tempo e tenta renderizar o conteúdo na tela.

As principais classes de erros a seguir podem ocorrer durante as seguintes fases:

* Ao conectar-se ao servidor host.
* Ao baixar o arquivo de manifesto.
* Ao baixar os segmentos de mídia.

O TVSDK encaminha os eventos acionados para seu aplicativo, incluindo eventos de notificação que são acionados quando:

* Ocorre um failover.
* O perfil foi alterado devido ao algoritmo de failover.
* Todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Independentemente de ocorrerem erros, chamadas TVSDK `onAdBreakComplete` para cada `onAdBreakStart` e `onAdComplete` para cada `onAdStart`. No entanto, se não for possível baixar os segmentos, poderá haver lacunas na linha do tempo. Quando as lacunas são grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
