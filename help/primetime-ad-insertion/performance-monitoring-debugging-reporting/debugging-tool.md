---
title: Ferramenta de depuração do servidor manifest
description: Ferramenta de depuração do servidor manifest
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# Ferramenta de depuração do servidor manifest {#manifest-server-debugging-tool}

A ferramenta de depuração permite que os editores investiguem problemas de inserção de anúncios potencialmente caros examinando as informações de depuração retornadas em tempo real pelo servidor de manifesto em cabeçalhos HTTP ou, quando forem necessárias informações mais detalhadas, examinando logs de sessão após o fato. Os parceiros do Adobe, como o Akamai, podem usar a ferramenta para depurar suas integrações com o Primetime ad decisioning.

A ferramenta suporta problemas de depuração e inserção em qualquer uma das principais configurações de rastreamento de anúncios do servidor de manifesto:

* Rastreamento do lado do cliente com um reprodutor com base em TVSDK.
* Rastreamento do lado do cliente com um reprodutor não baseado no TVSDK.
* Rastreamento no servidor.

Para ser compatível com todos esses casos, a ferramenta não requer ou usa códigos de editor de player.

Ao iniciar uma sessão de servidor de manifesto, você pode definir um parâmetro no URL da solicitação para solicitar que ele registre informações de depuração. Usando valores diferentes desse parâmetro, você também pode solicitar que o servidor de manifesto retorne partes especificadas das informações de depuração em cabeçalhos HTTP, mas os cabeçalhos podem conter apenas uma quantidade limitada de informações. Você pode obter credenciais do Adobe para acessar arquivos de log completos, que o servidor de manifesto salva periodicamente (por exemplo, a cada hora) em um servidor de arquivamento. Depois de ter credenciais para esse servidor, você poderá acessá-lo diretamente a qualquer momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opções de ferramenta de depuração {#debugging-tool-options}

Ao chamar a ferramenta de depuração, você tem várias opções para quais informações o servidor de manifesto retorna nos cabeçalhos HTTP. As opções não afetam o que o servidor manifest coloca nos arquivos de log.

### Especificação de depuração de patch {#specifying-ptdebug}

Ao iniciar o log de depuração para uma sessão de servidor de manifesto, você pode adicionar o parâmetro ptdebug ao URL da solicitação para especificar as seguintes opções para as informações que o servidor de manifesto retorna nos cabeçalhos HTTP:

* ptdebug=true Todos os registros exceto `TRACE_HTTP_HEADER` e a maioria `call/response data` de `TRACE_AD_CALL` registros.
* ptdebug=AdCall Somente TRACE_AD_*tipo* (por exemplo, TRACE_AD_CALL) registros.
* ptdebug=Header Somente registros TRACE_HTTP_HEADER.

As opções não afetam o que o servidor de manifesto posiciona nos arquivos de log. Você não tem controle sobre isso, mas os arquivos de log são arquivos de texto, portanto, você pode aplicar uma grande variedade de ferramentas para extrair e reformatar as informações que lhe interessam.

Veja um exemplo do cabeçalho HTTP retornado quando `ptdebug=Header`. Algumas sequências longas de dígitos hexadecimais são substituídas por `. . .` para maior clareza.

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## Formatos de registros de log {#formats-of-log-records}

Cada registro de log tem um tipo e um conjunto de campos, alguns dos quais podem ser opcionais. Os campos de todos os registros até o tipo de registro são os mesmos. Eles fornecem um carimbo de data e hora e informações sobre a sessão. O tipo de registro identifica o tipo de evento que está sendo registrado e os campos subsequentes fornecem informações sobre o evento registrado.

A estrutura de um registro de log é a seguinte:

`datetime request_id session_id zone_id record_type` *outros campos.*

| Campo | Tipo | Descrição |
|--- |--- |--- |
| datetime | string | Carimbo de data e hora |
| request_id | string | ID de solicitação usada pelo servidor de manifesto (carimbo de data e hora unix) |
| session_id | string | ID da sessão usada pelo servidor de manifesto |
| zone_id | integer | ID da Zona |
| record_type | string | Tipo de evento que está sendo registrado |
| outros campos | *** | Depender do tipo de evento |

### TRACE_REQUEST_INFO registra {#trace-request-info-records}

Registros desse tipo registram os resultados de solicitações HTTP. Os campos além de TRACE_REQUEST_INFO aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| request_method | string | Método HTTP (GET ou POST) |
| request_uri | string | URI de solicitação HTTP (sem host) |
| request_length | integer | Comprimento da solicitação (bytes) |
| response_length | integer | Comprimento da resposta (bytes) |
| delta | integer | Tempo (milissegundos) para processar a solicitação |
| module_type | string | Variante, fluxo ou VOD |
| remote_address_aud_client_ip | string | (ver nota) |
| remote_address_x_fwd_for_hdr_key | string | (ver nota) |
| remote_host_port | string | (ver nota) |

>[!NOTE]
>
>Os três últimos campos são opcionais.

Um exemplo:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER registra {#trace-http-header-records}

Registros desse tipo registram cabeçalhos HTTP de log trocados durante chamadas HTTP entre o servidor de manifesto e o cliente, o servidor de publicidade ou o servidor de conteúdo. Os campos além de TRACE_HTTP_HEADER aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| request_type | string | Tipo de solicitação (MAIN ou UNKNOWN) |
| request_response | string | Cabeçalho de resposta (solicitação ou resposta) |
| nome_do_cabeçalho | string | Nome do cabeçalho HTTP |
| header_value | string | Valor do cabeçalho HTTP codificado em Base64 |

>[!NOTE]
>
>Os campos request_type e header_value são opcionais.

Um exemplo:

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### TRACE_AD_CALL registra {#trace-ad-call-records}

Registros desse tipo registram os resultados de solicitações de anúncios do servidor de manifesto. Os campos além de TRACE_AD_CALL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| request_duration | integer | Tempo (milissegundos) da solicitação para a resposta |
| ad_server_query_url | string | URL da chamada de anúncio, incluindo parâmetros de consulta |
| ad_system_id | string | Sistema de anúncios, da resposta do servidor de anúncios (Auditude, se não especificado) |
| avail_id | string | ID do valor, da dica de anúncio no arquivo de manifesto de conteúdo (N/A para VOD) |
| avail_duration | número | Duração (segundos) do valor disponível, a partir da dica de anúncio no arquivo de manifesto de conteúdo (N/A para VOD) |
| ad_server_response | string | Resposta codificada em Base64 do servidor de anúncios |

Um exemplo:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT registram {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Registros desse tipo registram os resultados das solicitações de anúncios indicadas pelo tipo de registro. Os campos além do tipo de registro aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| avail_id | string | ID do disponível, da dica de anúncio no arquivo de manifesto de conteúdo (live) ou do servidor de manifesto (VOD) |
| ad_type | string | Tipo de anúncio (DIRETO ou REDIRECIONAMENTO) |
| ad_duration | integer | Duração (segundos) do anúncio, da resposta do servidor de anúncios |
| ad_content_url | string | URL do arquivo manifest do anúncio, da resposta do servidor de anúncios |
| ad_content_url_atual | string | URL do arquivo manifest da publicidade inserida. Vazio para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de anúncios, da resposta do servidor de anúncios (Auditude, se não especificado) |
| ad_id | string | ID do anúncio, da resposta do servidor de anúncios |
| creative_id | string | ID do criativo, no nó do anúncio, da resposta do servidor de anúncios |
| ad_call_id | string | Não usado. Reservado para uso futuro. |
| delta | integer | Tempo (milissegundos) utilizado por este evento |
| misc | string | Motivo do anúncio ignorado |

>[!NOTE]
>
>Os campos ad_content_url_actual, ad_call_id e misc são opcionais.

Para TRACE_AD_RESOLVE e TRACE_AD_INSERT, o URL no campo ad_content_url_real é para o anúncio transcodificado, se disponível. Caso contrário, o campo fica vazio para TRACE_AD_RESOLVE ou como ad_content_url para TRACE_AD_INSERT.

Um exemplo:

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### TRACE_TRACKING_URL registra {#trace-tracking-url-records}

Registros desse tipo registram os resultados de solicitações de anúncios do servidor de manifesto. Os campos além de TRACE_TRACKING_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| pts | número | Carimbo de data e hora do programa. Tempo no vídeo para chamar o URL. |
| ad_system | string | Sistema de anúncios (auditude ou roda livre) |
| url | string | URL pingado |
| status | string | Status HTTP retornado do ping |

Um exemplo:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registros {#trace-transcoding-no-media-to-transcode-records}

Registros desse tipo registram um anúncio ausente. O único campo além de TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE aparece na tabela.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| ad_id | string | ID de anúncio totalmente qualificado `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` PROTOCOLO: AUDITUDE, VAST) |

### TRACE_TRANSCODING_REQUESTED registra {#trace-transcoding-requested-records}

Registros desse tipo registram os resultados das solicitações de transcodificação que o servidor de manifesto envia para o CRS. Os campos além de TRACE_TRANSCODING_REQUESTED aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| ad_id | string | ID de anúncio totalmente qualificada |
| ad_manifest_url | string | URL do arquivo manifest do anúncio, da resposta do servidor de anúncios |
| creative_type | string | Tipo de mídia |
| sinalizadores | string | ID3 indica se a solicitação de transcodificação inclui uma solicitação para adicionar uma tag ID3 |
| target_duration | string | Duração do target (segundos) do anúncio transcodificado |

### TRACE_TRACKING_REQUEST registros {#trace-tracking-request-records}

Registros desse tipo indicam uma solicitação para fazer o rastreamento no lado do servidor. Os campos além de TRACE_TRACKING_REQUEST aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| tracking_url_count | integer | Número de URLs de rastreamento |
| start | float | Tempo de início do fragmento PTS (segundos com precisão de milissegundo) |
| end | float | Tempo de término do fragmento PTS (segundos com precisão de milissegundo) |

### TRACE_TRACKING_REQUEST_URL registra {#trace-tracking-request-url-records}

Os registros desse tipo fornecem um URL de rastreamento para o rastreamento do lado do servidor. Os campos além de TRACE_TRACKING_REQUEST_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| timestamp | float | Tempo (segundos, com precisão .001) na sessão de reprodução para enviar um ping ao URL de rastreamento |
| ad_system | string | Sistema de anúncios (por exemplo, auditude) |
| url | string | URL para ping |

### TRACE_WEBVTT_REQUEST registros {#trace-webvtt-request-records}

Registros desse tipo de solicitações de log que o servidor de manifesto faz para legendas WEBVTT. Os campos além de TRACE_WEBVTT_REQUEST aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| vtt_uri | string | URL para solicitação |
| start | float | Tempo de início dividido (segundos com precisão de milissegundos) |
| end | float | Tempo de término dividido (segundos com precisão de milissegundo) |

### TRACE_WEBVTT_RESPONSE registros {#trace-webvtt-response-records}

Registra ``of ``neste ``type ``registro ``responses ``o ``manifest ``servidor ``sends ``para ``clients ``em `` `answer` ``para ``requests `` `for` ``WEBVTT ``legendas. Os campos além de TRACE_WEBVTT_RESPONSE &quot;aparecem na ordem mostrada na tabela, separando `by`guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| response | string | Resposta codificada em Base64 enviada ao cliente |

### TRACE_WEBVTT_SOURCE registra {#trace-webvtt-source-records}

Registros desse tipo de resposta de log a solicitações feitas pelo servidor de manifesto para legendas WEBVTT. Os campos além de TRACE_WEBVTT_SOURCE aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| source | string | Conteúdo VTT original codificado em base64 |


### Registros TRACE_MISC {#trace-misc-records}

Registros desse tipo permitem que o servidor de manifesto registre eventos e informações não planejadas para quando assimilar anúncios. O campo além de TRACE_MISC consiste em uma string de mensagem. As mensagens que podem aparecer incluem:

* Anúncio ignorado : AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*segundos*, ignore=*ignore*, redirectAd=*redirectAd*, priority=*priority*
* O posicionamento do anúncio retornou nulo.
* Anúncio corrigido com êxito.
* Falha na chamada de anúncio : *mensagem de erro*.
* Adicionar User-Agent para buscar o manifesto bruto: *agente-usuário*.
* Adicionar cookie para buscar o manifesto bruto: [cookie]
* URL inválido *mensagem de erro de URL solicitada*. (Falha ao analisar o URL da variante)
* url chamado: URL *obter retorno: código de resposta*. (Live URL)
* url chamado: URL *código de retorno: código de resposta*. (URL VOD)
* Conflito encontrado ao resolver anúncios: ou um dos - início intermediário ou fim intermediário está inserido no precedente ou antes da exibição contido no VOD (mid-roll).
* Exceção sem tratamento detectada lançada pelo manipulador para URI: *solicitação de URL*.
* Criação de manifesto de variante concluída. (Variante)
* Criação de manifesto de variante concluída.
* Exceção na manipulação de redirecionamento VAST *URL de redirecionamento *erro: *mensagem de erro*.
* Falha ao buscar a lista de reprodução do anúncio para *URL de manifesto do anúncio*.
* Falha ao gerar manifesto direcionado. (HLSManifestResolver)
* Falha ao analisar a primeira resposta de chamada de anúncio: *mensagem de erro*.
* Falha ao processar *GET|POST *solicitação para caminho: *solicitação de URL*. (Live/VOD)
* Falha ao processar solicitação de manifesto ao vivo: *solicitação de URL*. (Ao vivo)
* Falha ao retornar um manifesto de variante: *mensagem de erro*.
* Falha ao validar ID de grupo: *ID de grupo*.
* Buscando manifesto bruto: *URL de conteúdo*. (Ao vivo)
* Após o redirecionamento VAST: *redirecionar URL*.
* Encontrado vazio disponível. (VOD)
* Encontrado *número *anúncios. (VOD)
* Solicitação HTTP recebida. (Mensagem muito inicial)
* Ignorando anúncio porque a diferença entre a duração da resposta do anúncio (*duração da resposta do anúncio *s) e a duração real do anúncio (*duração real *s) é maior que o limite. (HLSManifestResolver)
* Ignorando o valor que não forneceu o valor da ID. (GroupAdResolver.java)
* Ignorando o valor válido que forneceu o valor de tempo inválido: *time *for availId = *ID válido*.
* Ignorando o valor válido que forneceu o valor de duração inválido: *duration *for availId = *ID válido*.
* Inicializar nova sessão. (Variante)
* Método HTTP inválido. Deve ser uma GET. (VOD)
* Método HTTP inválido. A solicitação de rastreamento deve ser um GET. (Ao vivo)
* URL inválido *mensagem de erro de URL solicitada*. (Variante)
* Grupo inválido. (HLSManifestResolver)
* Solicitação inválida. Legenda não é uma solicitação de rastreamento válida. (VOD)
* Solicitação inválida. O pedido de legenda deve ser feito após o estabelecimento da sessão. (VOD)
* Solicitação inválida. A solicitação de rastreamento deve ser feita após o estabelecimento da sessão. (VOD)
* Instância de servidor inválida para ID de grupo de sobrecarga: *ID de grupo*. (Ao vivo)
* Limite de redirecionamentos VAST atingido - *number*.
* Fazer chamada de anúncio: *adicionar URL de chamada*.
* Não foi encontrado nenhum manifesto para: *URL de conteúdo*. (Ao vivo)
* Nenhum valor correspondente encontrado para a ID válida: *ID disponível*. (HLSManifestResolver)
* Nenhuma sessão de reprodução encontrada. (HLSManifestResolver)
* Processando solicitação VOD para manifesto *URL de conteúdo*.
* Variante de processamento.
* Processando solicitação de legenda para o manifesto *URL de conteúdo*.
* Processando solicitação de rastreamento. (VOD)
* Redirecionar resposta de anúncio vazia. (VASTStAX)
* Solicitação: *URL*.
* Resposta de erro de retorno para a solicitação do GET porque nenhuma sessão de reprodução foi encontrada. (VOD)
* Retornando resposta de erro para a solicitação GET devido a um erro interno do servidor.
* Resposta de erro de retorno para a solicitação do GET que especifica um ativo inválido: *ID da solicitação de anúncio*. (VOD)
* Resposta de erro de retorno para a solicitação do GET que especifica uma ID de grupo inválida ou vazia: *ID de grupo*. (VOD)
* Resposta de erro de retorno para a solicitação do GET que especifica um valor de posição de rastreamento inválido. (VOD)
* Resposta de erro de retorno para solicitação de GET com sintaxe inválida - *URL de solicitação*. (Live/VOD)
* Resposta de erro de retorno para a solicitação com método HTTP não suportado: *GET|POST*. (Live/VOD)
* Retornando manifesto do cache. (VOD)
* O servidor está sobrecarregado. Continue sem a solicitação do ponto de anúncio. (Variante)
* Comece a gerar o manifesto direcionado. (HLSManifestResolver)
* Comece gerando manifesto de variante a partir de: *URL de conteúdo*. (Variante)
* Comece a compilar anúncios em manifesto. (VODHLSResolver)
* Tentando compilar anúncio em `HH:MM:SS`: AdPlacement \[adManifestURL=*ad Manifest URL*, durationSeconds=*segundos*, ignore=*ignore*, redirectAd=*redirect ad*, priority=*priority*.\]
* Não é possível obter anúncios devido a uma linha de tempo inválida - retornou o conteúdo sem anúncios. (VOD)
* Não é possível obter anúncios - retornou o conteúdo sem anúncios. (VOD)
* Não é possível obter consulta de anúncio e nenhum URL de conteúdo foi fornecido. (VOD)
* URL válido recebido. (VOD/Variante)
* Variante M3U8 não encontrada. (Variante)

### TRACE_TRACKING_URL registra {#trace-tracking-url-records-1}

O servidor de manifesto gera registros desse tipo após chamar um URL de rastreamento durante o workflow de rastreamento do lado do servidor. Os campos além de TRACE_TRACKING_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| pts | número | Tempo PTS no fluxo |
| ad_system | string | Sistema de anúncios (auditude ou roda livre) |
| url | string | URL pingado |
| state | string | Código do status HTTP |

### TRACE_PLAYBACK_PROGRESS registra {#trace-playback-progress-records}

O servidor manifest gera registros desse tipo quando recebe um sinal sobre o progresso da reprodução durante o workflow de rastreamento do lado do servidor. Os campos além de TRACE_PLAYBACK_PROGRESS aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código do status HTTP |
| largura de banda | integer | Largura de banda do fluxo |
| pts | integer | Tempo PTS no fluxo |
| ms_time | integer | Tempo quando o servidor de manifesto gerou o URL de rastreamento |
| url | string | Redirecionar URL |
| header_user_agent | string | Cabeçalho do agente do usuário HTTP |
| header_dnt | integer | Cabeçalho de não rastreamento HTTP |
| effective_remote_address | string | Endereço remoto efetivo IPv4 |
| endereço_remoto | string | Endereço remoto IPv4 |

>[!NOTE]
>
>Os últimos quatro campos são opcionais.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
