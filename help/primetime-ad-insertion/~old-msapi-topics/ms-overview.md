---
description: O servidor de manifesto coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeo e rastreiam anúncios. Ele recebe listas de reprodução codificadas em M3U8 (manifestos) que os players de vídeo cliente recebem de provedores de conteúdo, une anúncios de provedores de anúncio aos manifestos e transmite os manifestos compilados para players de vídeo. Ele oferece suporte ao rastreamento de anúncios do lado do cliente e do lado do servidor. Ele conduz suas interações usando uma interface de serviço da Web baseada em HTTP.
title: Visão geral das interações do servidor de manifesto
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Visão geral das interações do servidor de manifesto {#overview-of-manifest-server-interactions}

O servidor de manifesto coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeo e rastreiam anúncios. Ele recebe listas de reprodução codificadas em M3U8 (manifestos) que os players de vídeo cliente recebem de provedores de conteúdo, une anúncios de provedores de anúncio aos manifestos e transmite os manifestos compilados para players de vídeo. Ele oferece suporte ao rastreamento de anúncios do lado do cliente e do lado do servidor. Ele conduz suas interações usando uma interface de serviço da Web baseada em HTTP.

Uma configuração típica contém:

* O servidor de manifesto Primetime
* O Serviço de reempacotamento criativo (CRS) do Primetime
* Um cliente, controle de um player de vídeo
* Um editor, geralmente com um Sistema de gerenciamento de conteúdo (CMS)
* Uma rede de entrega de conteúdo (CDN)
* Um servidor de publicidade
* Um receptor para relatórios de rastreamento de anúncios

O fluxo de trabalho varia com base em vários fatores, como se o CDN for Akamai ou se o cliente estiver executando o rastreamento de anúncios. Para obter um diagrama do fluxo de trabalho para rastreamento de anúncios do cliente, consulte [Fluxo de trabalho de rastreamento do lado do cliente](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

O servidor de manifesto interage com clientes de entrega de vídeo recebendo e respondendo a solicitações HTTP GET. As respostas são manifestos codificados em M3U8 que descrevem conteúdo compilado por anúncio, incluindo, opcionalmente, uma estrutura JSON ou VMAP (sidecar) com instruções detalhadas de rastreamento de anúncios (consulte [Formatos de arquivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Um fluxo de trabalho típico é semelhante ao seguinte:

1. O publicador envia o URL de conteúdo e as informações do servidor de publicidade para o cliente.
1. O cliente usa as informações do publicador para gerar um URL de servidor de manifesto e envia uma solicitação GET para esse URL. Isso é conhecido como URL do Bootstrap.
1. O servidor de manifesto estabelece uma sessão com o cliente.
1. O servidor de manifesto obtém manifestos de conteúdo do CDN, que podem incluir informações de ad break.
1. O servidor de manifesto redireciona o cliente para o manifesto principal/variante gerado para o cliente.

   >[!NOTE]
   >
   >Se os parâmetros de consulta do URL do Bootstrap contiverem o valor `pttrackingmode=simple` ou `ptplayer=ios-mobileweb` configuração, o servidor de manifesto retorna o URL do manifesto principal/variante em um objeto JSON e o cliente envia uma solicitação GET para esse URL do manifesto variante.

1. O cliente escolhe um fluxo no manifesto de variante gerado para reproduzir, enviando informações de anúncios para o servidor de manifesto.
1. O servidor de manifesto passa as informações fornecidas pelo cliente para o servidor de publicidade e recebe anúncios e URLs de rastreamento de anúncios do servidor de publicidade. Se um anúncio fornecido não estiver no formato HLS, o servidor de manifesto o o enviará ao CRS para conversão ao HLS.
1. O servidor de manifesto compila os anúncios no manifesto de conteúdo e envia o novo manifesto compilado para o cliente.
1. O cliente reproduz o conteúdo com os anúncios anexados e faz solicitações nos horários especificados para os URLs de rastreamento especificados.

A inserção de anúncios no Primetime é compatível com clientes em várias plataformas de entrega de vídeo. Nem todos os clientes são criados no pacote TVSDK do Primetime, mas todos os clientes enviam solicitações do GET para o mesmo URL básico. Os parâmetros de consulta distinguem uma solicitação do cliente de outra informando ao servidor de manifesto:

* o cliente que está fazendo o pedido,
* o que esse cliente deseja,
* e quais informações de rastreamento de anúncios fornecer.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

O servidor de manifesto usa o CORS (Cross-Origin Resource Sharing standard, padrão de compartilhamento de recursos entre origens). Ele procura um `Origin` nas solicitações que recebe. Se o cabeçalho estiver presente, ele responderá com

* `Access-Control-Allow-Origin: *`string do cabeçalho Origin`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

Caso contrário, ele responderá com:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`