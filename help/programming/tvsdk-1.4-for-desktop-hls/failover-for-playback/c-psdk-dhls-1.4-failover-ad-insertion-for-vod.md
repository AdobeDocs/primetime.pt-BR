---
description: O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.
seo-description: O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.
seo-title: Inserção de publicidade e failover para VOD
title: Inserção de publicidade e failover para VOD
uuid: 98505f63-ac43-4ff5-9f7b-895b6135df47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# Inserção de publicidade e failover para VOD{#advertising-insertion-and-failover-for-vod}

O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.

## Fase de resolução de anúncios {#section_0D45C6094D724B55868B48F9A3557A8B}

O TVSDK entra em contato com um serviço de delivery de anúncios, como a tomada de decisões de anúncios do Adobe Primetime, e tenta obter o arquivo principal da lista de reprodução que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor de anúncio remoto e analisa a resposta do servidor.

O TVSDK oferece suporte aos seguintes tipos de provedores de anúncios:

* Provedor de publicidade de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão do Primetime

   O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de definição de metas e um número de identificação do ativo, para o servidor back-end de decisão do anúncio Primetime. A decisão do anúncio Primetime responde com um documento SMIL (sincronized multimedia integration language) que contém as informações necessárias do anúncio.

Uma das seguintes situações de failover pode ocorrer durante essa fase:

* Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou erro no lado do servidor, como um recurso não encontrado e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

   Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de inserção de anúncio {#section_1B18E8B5768B4873B3346294175B7340}

O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios estiver concluída, o TVSDK terá uma lista ordenada de recursos de anúncios que são agrupados em quebras de anúncios. Cada quebra de anúncio é posicionada na linha do tempo do conteúdo principal usando um valor de start-tempo que é expresso em milissegundos (ms). Cada anúncio em uma quebra de anúncio tem uma propriedade de duração que também é expressa em ms. Os anúncios em intervalos de anúncios são encadeados um após o outro. Como resultado, a duração de um intervalo de anúncios é igual à soma das durações dos anúncios individuais que compõem os anúncios.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de tempo/duração de start de quebra de anúncio, os segmentos de anúncio podem se sobrepor. A sobreposição ocorre quando a última parte de um intervalo de anúncios faz interseção com o início do primeiro anúncio no próximo intervalo de anúncios. Nessas situações, descarta o intervalo posterior do anúncio e continua o processo de inserção do anúncio com o próximo item na lista até que todas as quebras de anúncio sejam inseridas ou descartadas.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de reprodução de anúncios {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

O TVSDK baixa os segmentos do anúncio e os renderiza na tela do dispositivo.

Nesse ponto, o TVSDK resolveu os anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As seguintes classes principais de erros podem ocorrer nesta fase:

* Erros ao conectar ao servidor host
* Erros ao baixar o arquivo manifest
* Erros ao baixar segmentos de mídia

Para todas as três classes de erro, o TVSDK encaminhou eventos para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Eventos de notificação acionados quando todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Independentemente de ocorrerem erros, o TVSDK chama `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` para cada `AdBreakPlaybackEvent.AD_BREAK_STARTED` e `AdPlaybackEvent.AD_COMPLETED` para cada `AdPLaybackEvent.AD_STARTED`. No entanto, se os segmentos não puderem ser baixados, pode haver lacunas na linha do tempo. Quando as lacunas forem grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
