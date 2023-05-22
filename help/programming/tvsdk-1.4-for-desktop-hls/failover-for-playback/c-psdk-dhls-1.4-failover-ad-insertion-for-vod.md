---
description: O processo de inserção de anúncios de vídeo sob demanda (VOD) consiste nas fases de resolução, inserção e reprodução de anúncios. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o progresso da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas adequadas.
title: Inserção de publicidade e failover para VOD
exl-id: 5af5bef6-e948-4215-a89f-ee46fd2d8a38
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Inserção de publicidade e failover para VOD{#advertising-insertion-and-failover-for-vod}

O processo de inserção de anúncios de vídeo sob demanda (VOD) consiste nas fases de resolução, inserção e reprodução de anúncios. Para o rastreamento de anúncios, o TVSDK deve informar um servidor de rastreamento remoto sobre o progresso da reprodução de cada anúncio. Quando surgem situações inesperadas, toma as medidas adequadas.

## Fase de resolução de anúncios {#section_0D45C6094D724B55868B48F9A3557A8B}

O TVSDK entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.

O TVSDK é compatível com os seguintes tipos de provedores de anúncios:

* Provedor de anúncio de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão de anúncio do Primetime

   O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de direcionamento e um número de identificação de ativo, para o servidor back-end do Primetime ad Decisioning. O Primetime ad Decisioning responde com um documento SMIL (linguagem de integração multimídia sincronizada) que contém as informações de anúncio necessárias.

Uma das seguintes situações de failover pode ocorrer durante essa fase:

* Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou um erro do lado do servidor, como a impossibilidade de encontrar um recurso e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

   Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de inserção do anúncio {#section_1B18E8B5768B4873B3346294175B7340}

O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios for concluída, o TVSDK terá uma lista ordenada de recursos de anúncios agrupados em ad breaks. Cada ad break é posicionado na linha do tempo do conteúdo principal usando um valor de hora de início expresso em milissegundos (ms). Cada anúncio em um ad break tem uma propriedade de duração que também é expressa em ms. Os anúncios em um ad break são encadeados um após o outro. Como resultado, a duração de um ad break é igual à soma das durações dos anúncios compostos individuais.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de hora de início/duração do ad break, os segmentos de anúncios podem se sobrepor. A sobreposição ocorre quando a última parte de um ad break intercepta o início do primeiro anúncio no próximo ad break. Nessas situações, o descarta o ad break posterior e continua o processo de inserção de anúncio com o próximo item na lista até que todos os ad breaks sejam inseridos ou descartados.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.

## Fase de reprodução do anúncio {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

O TVSDK baixa os segmentos de anúncios e os renderiza na tela do dispositivo.

Nesse ponto, o TVSDK resolveu anúncios, os posicionou na linha do tempo e tenta renderizar o conteúdo na tela.

As principais classes de erros a seguir podem ocorrer nesta fase:

* Erros ao conectar-se ao servidor host
* Erros ao baixar o arquivo de manifesto
* Erros ao baixar os segmentos de mídia

Para todas as três classes de erro, o TVSDK encaminha eventos acionados para seu aplicativo, incluindo:

* Eventos de notificação acionados quando ocorre um failover.
* Eventos de notificação quando o perfil é alterado devido ao algoritmo de failover.
* Os eventos de notificação são acionados quando todas as opções de failover são consideradas e nenhuma ação adicional pode ser executada automaticamente.

   Seu aplicativo precisa tomar a ação apropriada.

Ocorrem ou não erros, chamadas TVSDK `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` para cada `AdBreakPlaybackEvent.AD_BREAK_STARTED` e `AdPlaybackEvent.AD_COMPLETED` para cada `AdPLaybackEvent.AD_STARTED`. No entanto, se não for possível baixar os segmentos, poderá haver lacunas na linha do tempo. Quando as lacunas são grandes o suficiente, os valores na posição do indicador de reprodução e o progresso do anúncio relatado podem exibir descontinuidades.
