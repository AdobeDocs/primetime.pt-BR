---
description: O servidor manifest coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeos e rastreiam anúncios. Ele recebe playlists codificadas em M3U8 (manifestos) que os players de vídeo cliente recebem de provedores de conteúdo, reúne anúncios de provedores de anúncios nos manifestos e transmite os manifestos com pontos para os players de vídeo. Ele oferece suporte ao rastreamento de anúncios do lado do cliente e do lado do servidor. Ele realiza suas interações usando uma interface de serviço da Web baseada em HTTP.
seo-description: O servidor manifest coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeos e rastreiam anúncios. Ele recebe playlists codificadas em M3U8 (manifestos) que os players de vídeo cliente recebem de provedores de conteúdo, reúne anúncios de provedores de anúncios nos manifestos e transmite os manifestos com pontos para os players de vídeo. Ele oferece suporte ao rastreamento de anúncios do lado do cliente e do lado do servidor. Ele realiza suas interações usando uma interface de serviço da Web baseada em HTTP.
seo-title: Visão geral das interações do servidor manifest
title: Visão geral das interações do servidor manifest
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: 9dc8498593a1d70918b66016e429eb013cdc61f7

---


# Visão geral das interações do servidor manifest {#overview-of-manifest-server-interactions}

O servidor manifest coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeos e rastreiam anúncios. Ele recebe playlists codificadas em M3U8 (manifestos) que os players de vídeo cliente recebem de provedores de conteúdo, reúne anúncios de provedores de anúncios nos manifestos e transmite os manifestos com pontos para os players de vídeo. Ele oferece suporte ao rastreamento de anúncios do lado do cliente e do lado do servidor. Ele realiza suas interações usando uma interface de serviço da Web baseada em HTTP.

Uma configuração típica contém:

* O servidor manifest Primetime
* O Serviço de Reembalagem Criativa Primetime (CRS)
* Um cliente, controlando um player de vídeo
* Um editor, geralmente com um Sistema de Gerenciamento de Conteúdo (CMS)
* Uma Rede de Entrega de Conteúdo (CDN)
* Um servidor de publicidade
* Um receptor para relatórios de rastreamento de anúncio

O fluxo de trabalho varia com base em vários fatores, como se o CDN for Akamai, ou se o cliente estiver realizando o rastreamento de anúncios. Para obter um diagrama do fluxo de trabalho do rastreamento de anúncios do cliente, consulte Fluxo de trabalho [](../msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow)do rastreamento do cliente.

O servidor manifest interage com os clientes de entrega de vídeo ao receber e responder às solicitações HTTP GET. As respostas são manifestos codificados em M3U8 que descrevem o conteúdo com pontos de anúncio, incluindo opcionalmente uma estrutura JSON ou VMAP (auxiliar) que contém instruções detalhadas de rastreamento de anúncio (consulte Formatos [de](../msapi-topics/ms-list-file-formats/ms-api-file-formats.md)arquivo).

Um fluxo de trabalho típico tem a seguinte aparência:

1. O editor envia o URL de conteúdo e as informações do servidor de publicidade para o cliente.
1. O cliente usa as informações do editor para gerar um URL de servidor manifest e envia uma solicitação GET para esse URL. Isso é conhecido como o URL do Bootstrap.
1. O servidor manifest estabelece uma sessão com o cliente.
1. O servidor manifest obtém manifestos de conteúdo do CDN, que podem incluir informações de quebra de anúncio.
1. O servidor manifest redireciona o cliente para o manifesto mestre/variante que ele gerou para o cliente.

   >[!NOTE]
   >
   >Se os parâmetros de consulta de URL do Bootstrap contiverem a configuração `pttrackingmode=simple` ou `ptplayer=ios-mobileweb` , o servidor manifest retornará o URL do manifesto mestre/variante em um objeto JSON e o cliente enviará uma solicitação GET para esse URL do manifesto da variante.

1. O cliente escolhe um fluxo no manifesto de variante gerado para reproduzir, enviando informações de publicidade para o servidor de manifesto.
1. O servidor manifest transmite as informações fornecidas pelo cliente para o servidor de publicidade e recebe anúncios e URLs de rastreamento de anúncios do servidor de publicidade. Se um anúncio fornecido não estiver no formato HLS, o servidor manifest o enviará para CRS para conversão para HLS.
1. O servidor manifest agrupa anúncios no manifesto do conteúdo e envia o novo manifesto unido para o cliente.
1. O cliente reproduz o conteúdo com os anúncios agrupados e faz solicitações nos horários especificados para os URLs de rastreamento especificados.

A inserção de anúncios do Primetime é compatível com clientes em várias plataformas de entrega de vídeo. Nem todos os clientes são criados no pacote Primetime TVSDK, mas todos os clientes enviam solicitações GET para o mesmo URL básico. Os parâmetros de consulta distinguem uma solicitação de cliente da outra informando ao servidor manifest:

* qual cliente está a apresentar o pedido,
* o que esse cliente quer,
* e quais informações de rastreamento de anúncios devem ser fornecidas.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

O servidor manifest usa o CORS (Cross-Origin Resource Sharing Standard). Ele procura um `Origin` cabeçalho nas solicitações que recebe. Se o cabeçalho estiver presente, ele responderá com

* `Access-Control-Allow-Origin: *`string do cabeçalho Origem`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

Em caso negativo, responde com:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`