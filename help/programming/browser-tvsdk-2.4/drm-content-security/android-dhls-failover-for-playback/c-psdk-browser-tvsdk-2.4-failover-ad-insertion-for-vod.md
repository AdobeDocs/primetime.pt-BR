---
description: O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK do navegador deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.
seo-description: O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK do navegador deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.
seo-title: Inserção de publicidade e failover para VOD
title: Inserção de publicidade e failover para VOD
uuid: 33f7aad5-fc4f-459d-8c29-01ba1353dfcc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---


# Inserção de publicidade e failover para VOD{#advertising-insertion-and-failover-for-vod}

O processo de inserção de anúncio por demanda (VOD) consiste nas fases de resolução, inserção e reprodução do anúncio. Para o rastreamento de anúncios, o TVSDK do navegador deve informar um servidor de rastreamento remoto sobre o andamento da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas apropriadas.

## Fase de resolução de anúncios {#section_F562CD6D0EF04AA9A0A3C0176A4EC340}

O TVSDK do navegador entra em contato com um serviço de delivery de anúncio, como a tomada de decisão de anúncio do Adobe Primetime, e tenta obter o arquivo principal da lista de reprodução que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK do navegador faz uma chamada HTTP para o servidor de anúncio remoto e analisa a resposta do servidor.

O TVSDK do navegador suporta os seguintes tipos de provedores de anúncios:

* Provedor de publicidade de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão da Adobe Primetime

   O TVSDK do navegador envia uma solicitação, incluindo um conjunto de parâmetros de definição de metas e um número de identificação de ativo, para o servidor back-end de decisão de anúncio da Adobe Primetime. A decisão do anúncio da Adobe Primetime responde com um documento SMIL (sincronized multimedia integration language) que contém as informações necessárias do anúncio.

   Uma das seguintes situações de failover pode ocorrer durante essa fase:

   * Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou erro no lado do servidor, como um recurso não encontrado e assim por diante.
   * Os dados foram recuperados, mas o formato é inválido.

      Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.
   O TVSDK do navegador emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de inserção de anúncio {#section_88A0E4FA12394717A9D85689BD11D59F}

O TVSDK do navegador insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios estiver concluída, o TVSDK do navegador terá uma lista ordenada de recursos de anúncios que são agrupados em quebras de anúncios. Cada quebra de anúncio é posicionada na linha do tempo do conteúdo principal usando um valor de start-tempo que é expresso em milissegundos (ms). Cada anúncio em uma quebra de anúncio tem uma propriedade de duração que também é expressa em ms. Os anúncios em intervalos de anúncios são encadeados um após o outro. Como resultado, a duração de um intervalo de anúncios é igual à soma das durações dos anúncios individuais que compõem os anúncios.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de tempo/duração de start de quebra de anúncio, os segmentos de anúncio podem se sobrepor. A sobreposição ocorre quando a última parte de um intervalo de anúncios faz interseção com o início do primeiro anúncio no próximo intervalo de anúncios. Nessas situações, o TVSDK do navegador descarta o intervalo posterior do anúncio e continua o processo de inserção do anúncio com o próximo item na lista até que todas as quebras do anúncio sejam inseridas ou descartadas.

O TVSDK do navegador emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de reprodução de anúncios {#section_7B0073BE9A744C74929263182C1243FC}

O TVSDK do navegador baixa os segmentos do anúncio e os renderiza na tela do dispositivo.

Nesse ponto, o TVSDK do navegador resolveu os anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As seguintes classes principais de erros podem ocorrer nesta fase:

* Erros ao conectar ao servidor host
* Erros ao baixar o arquivo manifest
* Erros ao baixar segmentos de mídia

Para todas as três classes de erro, o TVSDK do navegador acionou eventos para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Eventos de notificação acionados quando todas as opções de failover foram consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Independentemente de erros ocorrerem ou não, o TVSDK do navegador notifica quando um start de quebra de anúncio é concluído. No entanto, se os segmentos não puderem ser baixados, pode haver lacunas na linha do tempo. Quando as lacunas forem grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
