---
description: O servidor de manifesto coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeo e rastreiam anúncios. Ele recebe listas de reprodução codificadas em M3U8 (manifestos) que os players de vídeo do cliente recebem de provedores de conteúdo, compila anúncios de provedores de anúncios nos manifestos e transmite os manifestos compilados para os players de vídeo. Ele é compatível com o rastreamento de anúncios do lado do cliente e do lado do servidor. Ele realiza suas interações usando uma interface de serviço da Web baseada em HTTP.
title: Visão geral das interações do Servidor de manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Visão geral das interações do Servidor de manifesto {#overview-of-manifest-server-interactions}

O servidor de manifesto coordena os sistemas que fornecem conteúdo, fornecem anúncios, reproduzem vídeo e rastreiam anúncios. Ele recebe listas de reprodução codificadas em M3U8 (manifestos) que os players de vídeo do cliente recebem de provedores de conteúdo, compila anúncios de provedores de anúncios nos manifestos e transmite os manifestos compilados para os players de vídeo. Ele é compatível com o rastreamento de anúncios do lado do cliente e do lado do servidor. Ele realiza suas interações usando uma interface de serviço da Web baseada em HTTP.

Uma configuração típica contém:

* O servidor manifest do Primetime
* O Serviço de Reempacotamento Criativo do Primetime (CRS)
* Um cliente, controlando um reprodutor de vídeo
* Um editor, geralmente com um Sistema de gerenciamento de conteúdo (CMS)
* Uma Rede de entrega de conteúdo (CDN)
* Um servidor de anúncios
* Um destinatário para relatórios de rastreamento de anúncios

O fluxo de trabalho varia com base em vários fatores, como se a CDN fosse Akamai, ou se o cliente estivesse executando o rastreamento de anúncios. Para obter um diagrama do fluxo de trabalho para o rastreamento de anúncios do lado do cliente, consulte [Fluxo de trabalho de rastreamento do lado do cliente](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

O servidor de manifesto interage com clientes de entrega de vídeo ao receber e responder solicitações HTTP GET. As respostas são manifestos codificados em M3U8 que descrevem o conteúdo anexado, opcionalmente incluindo uma estrutura JSON ou VMAP (sidecar) contendo instruções detalhadas de rastreamento de anúncio (consulte [Formatos de arquivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Um fluxo de trabalho típico tem a seguinte aparência:

1. O editor envia o URL de conteúdo e as informações do servidor de publicidade para o cliente.
1. O cliente usa as informações do editor para gerar um URL de servidor de manifesto e envia uma solicitação de GET para esse URL. Isso é conhecido como URL do Bootstrap.
1. O servidor manifest estabelece uma sessão com o cliente.
1. O servidor de manifesto obtém manifestos de conteúdo do CDN, que podem incluir informações de ad break.
1. O servidor manifest redireciona o cliente para o manifesto principal/variante que ele gerou para o cliente.

   >[!NOTE]
   >
   >Se os parâmetros de consulta de URL do Bootstrap contiverem a configuração `pttrackingmode=simple` ou `ptplayer=ios-mobileweb` , o servidor de manifesto retornará o URL de manifesto principal/variante em um objeto JSON e o cliente enviará uma solicitação de GET para esse URL de manifesto de variante.

1. O cliente escolhe um fluxo no manifesto de variante gerado para reproduzir, enviando informações de anúncio para o servidor de manifesto.
1. O servidor de manifesto transmite as informações fornecidas pelo cliente para o servidor de anúncios e recebe anúncios e URLs de rastreamento de anúncios do servidor de anúncios. Se um anúncio fornecido não estiver no formato HLS, o servidor de manifesto o enviará para o CRS para conversão para HLS.
1. O servidor manifest compila anúncios no manifesto do conteúdo e envia o novo manifesto compilado para o cliente.
1. O cliente reproduz o conteúdo com os anúncios anexados e faz solicitações, nos horários especificados, aos URLs de rastreamento especificados.

A inserção de anúncio do Primetime é compatível com clientes em muitas plataformas de entrega de vídeo. Nem todos os clientes são criados no pacote Primetime TVSDK, mas todos os clientes enviam solicitações do GET para o mesmo URL básico. Os parâmetros de consulta distinguem uma solicitação de cliente da outra, informando ao servidor manifest:

* que cliente está a apresentar o pedido,
* o que esse cliente quer,
* e quais informações de rastreamento de anúncios fornecer.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

O servidor de manifesto usa o CORS (Cross-Origin Resource Sharing standard). Ele procura um cabeçalho `Origin` nas solicitações que recebe. Se o cabeçalho estiver presente, ele responderá com

* `Access-Control-Allow-Origin: *`string do cabeçalho Origem`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

Caso contrário, responde com:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`