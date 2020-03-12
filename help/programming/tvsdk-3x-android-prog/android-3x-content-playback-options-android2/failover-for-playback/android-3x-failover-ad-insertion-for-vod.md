---
description: O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgirem situações inesperadas, o TVSDK toma as medidas apropriadas.
seo-description: O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgirem situações inesperadas, o TVSDK toma as medidas apropriadas.
seo-title: Inserção de publicidade e failover para VOD
title: Inserção de publicidade e failover para VOD
uuid: 74cc35e6-6479-4572-a3b3-05ff6344272a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Inserção de publicidade e failover para VOD {#advertising-insertion-and-failover-for-vod}

O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgirem situações inesperadas, o TVSDK toma as medidas apropriadas.

## Fase de resolução de anúncios {#section_5DD3A7DA79E946298BFF829A60202E1C}

O TVSDK entra em contato com um serviço de entrega de anúncios, como a decisão do anúncio do Adobe Primetime, e tenta obter o arquivo principal da lista de reprodução que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK efetua uma chamada HTTP para o servidor de entrega de anúncios remoto e analisa a resposta do servidor.

O TVSDK oferece suporte aos seguintes tipos de provedores de anúncios:

* Provedor de publicidade de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão do Primetime

   O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de definição de metas e um número de identificação do ativo, para o servidor back-end de decisão do Primetime e do Analytics. A decisão do anúncio Primetime responde a um documento SMIL (Ssynchronized multimedia integration language) que contém as informações necessárias do anúncio.
* Provedor personalizado de marcadores de anúncio

   Gerencia a situação em que os anúncios são gravados no stream, a partir do servidor. O TVSDK não executa a inserção real do anúncio, mas precisa rastrear os anúncios que foram inseridos no servidor. Esse provedor define os marcadores de anúncio que o TVSDK usa para executar o rastreamento de anúncio.

Uma das seguintes situações de failover pode ocorrer durante essa fase:

* Os dados não podem ser recuperados devido, por exemplo, à falta de conectividade ou a um erro do lado do servidor, como um recurso não encontrado, e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

   Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de inserção de anúncios {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios estiver concluída, o TVSDK terá uma lista ordenada de recursos de anúncios que são agrupados em quebras de anúncios. Cada quebra de anúncio é posicionada na linha do tempo do conteúdo principal usando um valor de hora de início expresso em milissegundos (ms). Cada anúncio em uma quebra de anúncio tem uma propriedade de duração que também é expressa em ms. Os anúncios em uma quebra de anúncio são encadeados e, como resultado, a duração de uma quebra de anúncio é igual à soma das durações dos anúncios individuais de composição.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de tempo de início/duração de quebra de anúncio, os segmentos de anúncio podem se sobrepor. Essa sobreposição ocorre quando a última parte de um intervalo de anúncios faz interseção com o início do primeiro anúncio no próximo intervalo de anúncios. Nessas situações, o TVSDK descarta o intervalo posterior do anúncio e continua o processo de inserção do anúncio com o próximo item na lista até que todas as quebras do anúncio sejam inseridas ou descartadas.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de reprodução do anúncio {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

O TVSDK baixa os segmentos do anúncio e os renderiza na tela do dispositivo.

Agora, o TVSDK resolveu os anúncios, posicionou os anúncios na linha do tempo e tenta renderizar o conteúdo na tela.

As seguintes classes principais de erros podem ocorrer durante as seguintes fases:

* Ao conectar-se ao servidor host.
* Ao baixar o arquivo manifest.
* Ao baixar os segmentos de mídia.

O TVSDK encaminha os eventos acionados para seu aplicativo, incluindo eventos de notificação que são acionados quando:

* Ocorre um failover.
* O perfil é alterado devido ao algoritmo de failover.
* Todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar as medidas apropriadas.

Independentemente de ocorrerem erros, o TVSDK chama `onAdBreakComplete` cada um `onAdBreakStart` e `onAdComplete` para cada `onAdStart`. No entanto, se os segmentos não puderem ser baixados, pode haver lacunas na linha do tempo. Quando as lacunas forem grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.