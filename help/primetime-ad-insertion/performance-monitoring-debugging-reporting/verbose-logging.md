---
title: Registro detalhado
description: Registro detalhado
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 0%

---

# Registro detalhado {#verbose-logging}

## descrições de eventos de depuração/registro {#ptdebug-logging-events}

Ao iniciar o log de depuração para uma sessão de servidor de manifesto, você pode adicionar o parâmetro `ptdebug` ao URL da solicitação para especificar as seguintes opções para as informações que o servidor de manifesto retorna nos cabeçalhos HTTP:

* `ptdebug=true`
Todos os registros, exceto TRACE_HTTP_HEADER e a maioria dos dados de chamada/resposta dos registros TRACE_AD_CALL.

* `ptdebug=AdCall`
Somente TRACE_AD_ type (por exemplo, TRACE_AD_CALL) registros.

* `ptdebug=Header`
Somente registros TRACE_HTTP_HEADER.

## Formatos de registros de log {#log-record-formats}

Cada registro de log tem um tipo e um conjunto de campos, alguns dos quais podem ser opcionais. Os campos de todos os registros até o tipo de registro são os mesmos. Eles fornecem um carimbo de data e hora e informações sobre a sessão. O tipo de registro identifica o tipo de evento que está sendo registrado e os campos subsequentes fornecem informações sobre o evento registrado.

A estrutura de um registro de log é a seguinte:

`datetime request_id session_id zone_id record_type other fields`.

| Campo | Tipo | Descrição |
|---|---|---|
| datetime | string | Carimbo de data e hora |
| request_id | string | ID da solicitação usada pelo servidor de manifesto (carimbo de data e hora Unix) |
| session_id | string | ID da sessão usada pelo servidor de manifesto |
| zone_id | integer | Zona |
| record_type | string | Tipo de evento que está sendo registrado |
| outros campos | varia | Depender do tipo de evento |

Registros desse tipo registram os resultados de solicitações HTTP. Os campos além de `TRACE_REQUEST_INFO` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| request_method | string | Método HTTP (GET ou POST) |
| request_uri | string | URI de solicitação HTTP (sem host) |
| request_length | integer | Comprimento da solicitação (bytes) |
| response_length | integer | Comprimento da resposta (bytes) |
| delta | integer | Tempo (milissegundos) para processar a solicitação |
| module_type | string | Variante, fluxo ou VOD |
| remote_address_aud_client_ip | string | **‡** |
| remote_address_x_fwd_for_hdr_key | string | **‡** |
| remote_host_port | string | **‡** |

**‡** Os três últimos campos são opcionais.

**Um exemplo**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER registra {#trace-http-header-records}

Registros desse tipo registram cabeçalhos HTTP de log trocados durante chamadas HTTP entre o servidor de manifesto e o cliente, o servidor de publicidade ou o servidor de conteúdo. Os campos além de TRACE_HTTP_HEADER aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| request_type | string | Tipo de solicitação (MAIN ou UNKNOWN) |
| request_response | string | Cabeçalho de resposta (solicitação ou resposta) |
| nome_do_cabeçalho | string | Nome do cabeçalho HTTP |
| header_value | string | Valor do cabeçalho HTTP codificado em Base64 |

>[!NOTE]
>
>Os campos `request_type` e `header_value` são opcionais.

**Um exemplo**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### TRACE_AD_CALL registra {#tracing-ad-call-records}

Registros desse tipo registram os resultados de solicitações de anúncios do servidor de manifesto. Os campos além de `TRACE_AD_CALL` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| request_duration | integer | Tempo (milissegundos) da solicitação para a resposta |
| ad_server_query_url | string | URL da chamada de anúncio, incluindo parâmetros de consulta |
| ad_system_id | string | Sistema de anúncios, da resposta do servidor de anúncios (Auditude, se não especificado) |
| avail_id | string | ID do valor, da dica de anúncio no arquivo de manifesto de conteúdo (N/A para VOD) |
| avail_duration | número | Duração (segundos) do valor disponível, a partir da dica de anúncio no arquivo de manifesto de conteúdo (N/A para VOD) |
| ad_server_response | string | Resposta codificada em Base64 do servidor de anúncios |

Um exemplo:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT registram {#trace-ad-insert-resolve-redirect}

Registros desse tipo registram os resultados das solicitações de anúncios indicadas pelo tipo de registro. Os campos além do tipo de registro aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado. |
| avail_id | string | ID do valor, da dica de anúncio no arquivo de manifesto de conteúdo (live) ou do servidor de manifesto (VOD). |
| ad_type | string | Tipo de anúncio (DIRETO ou REDIRECIONAMENTO). |
| ad_duration | integer | Duração (segundos) do anúncio, da resposta do servidor de anúncios. |
| ad_content_url | string | URL do arquivo manifest do anúncio, da resposta do servidor de anúncios. |
| **†** ad_content_url_actual | string | URL do arquivo manifest da publicidade inserida. Vazio para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de anúncios, da resposta do servidor de anúncios (Auditude, se não especificado). |
| ad_id | string | ID do anúncio, da resposta do servidor de anúncios. |
| creative_id | string | ID do criativo, do nó do anúncio, da resposta do servidor de anúncios. |
| **†** ad_call_id | string | Não usado. Reservado para uso futuro. |
| delta | integer | Tempo (milissegundos) utilizado por este evento. |
| **†** misc | string | O motivo do anúncio foi ignorado. |

**†** `ad_content_url_actual`,  `ad_call_id`e  `misc` os campos são opcionais.

>[!NOTE]
>
>Para `TRACE_AD_RESOLVE` e `TRACE_AD_INSERT`, o URL no campo `ad_content_url_actual` é para o anúncio transcodificado, se disponível. Caso contrário, o campo fica vazio para `TRACE_AD_RESOLVE` ou é o mesmo que `ad_content_url` para `TRACE_AD_INSERT`.

Um exemplo:

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registros {#trace-transcoding-no-media-to-transcode}

Registros desse tipo registram um anúncio ausente. O único campo além de `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` aparece na tabela.

| Campo | Tipo | Descrição |
|---|---|---|
| ad_id | string | ID de anúncio totalmente qualificada (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOLO:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLO: AUDITUDE, VAST) |

Registros desse tipo registram os resultados das solicitações de transcodificação que o servidor de manifesto envia para o CRS. Os campos além de `TRACE_TRANSCODING_REQUESTED` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| ad_id | string | ID de anúncio totalmente qualificada |
| ad_manifest_url | string | URL do arquivo manifest do anúncio, da resposta do servidor de anúncios |
| creative_type | string | Tipo de mídia |
| sinalizadores | string | ID3 indica se a solicitação de transcodificação inclui uma solicitação para adicionar uma tag ID3 |
| target_duration | string | Duração do target (segundos) do anúncio transcodificado |

Registros desse tipo indicam uma solicitação para fazer o rastreamento no lado do servidor. Os campos além de `TRACE_TRACKING_REQUEST` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| tracking_url_count | integer | Número de URLs de rastreamento |
| start | float | Tempo de início do fragmento PTS (segundos com precisão de milissegundo) |
| end | float | Tempo de término do fragmento PTS (segundos com precisão de milissegundo) |

Os registros desse tipo fornecem um URL de rastreamento para o rastreamento do lado do servidor. Os campos além de `TRACE_TRACKING_REQUEST_URL` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| timestamp | float | Tempo (segundos, com precisão de .001) na sessão de reprodução para fazer ping no URL de rastreamento. |
| ad_system | string | Sistema de anúncios (por exemplo, auditude) |
| url | string | URL para ping |

Registros desse tipo de solicitações de log que o servidor de manifesto faz para legendas `WEBVTT`. Os campos além de `TRACE_WEBVTT_REQUEST` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| vtt_uri | string | URL para solicitação |
| start | float | Tempo de início dividido (segundos com precisão de milissegundos) |
| end | float | Tempo de término dividido (segundos com precisão de milissegundo) |

Registros desse tipo de resposta de log que o servidor de manifesto envia aos clientes em `answer` para solicitações de `WEBVTT` legendas. Os campos além de `TRACE_WEBVTT_RESPONSE` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| response | string | Resposta codificada em Base64 enviada ao cliente |

Registros desse tipo de resposta de log a solicitações feitas pelo servidor de manifesto para legendas `WEBVTT`. Os campos além de `TRACE_WEBVTT_SOURCE` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| source | string | Conteúdo VTT original codificado em base64 |

Registros desse tipo permitem que o servidor de manifesto registre eventos e informações não planejadas para quando assimilar anúncios. O campo além de `TRACE_MISC` consiste em uma string de mensagem. As mensagens que podem aparecer incluem:

* Anúncio ignorado: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* O posicionamento do anúncio retornou nulo.
* Anúncio corrigido com êxito.
* Falha na chamada de anúncio : mensagem de erro.
* Adicionar User-Agent para buscar o manifesto bruto: agente-usuário.
* Adicionar cookie para buscar o manifesto bruto: #
* URL inválido solicitou mensagem de erro de URL. (Falha ao analisar o URL da variante)
* url chamado: URL recebe retorno: código de resposta. (Live URL)
* url chamado: Código de retorno de URL: código de resposta. (URL VOD)
* Conflito encontrado ao resolver anúncios: ou um dos - início intermediário ou fim intermediário está inserido no precedente ou antes da exibição contido no VOD (mid-roll).
* Exceção sem tratamento detectada lançada pelo manipulador para URI: URL da solicitação.
* Criação de manifesto de variante concluída. (Variante)
* Criação de manifesto de variante concluída.
* Exceção na manipulação de redirecionamento VAST *URL de redirecionamento *erro: mensagem de erro.
* Falha ao buscar a lista de reprodução do anúncio para o URL de manifesto do anúncio.
* Falha ao gerar manifesto direcionado. (HLSManifestResolver)
* Falha ao analisar a primeira resposta de chamada de anúncio: mensagem de erro.
* Falha ao processar *GET|POST *solicitação para caminho: URL da solicitação. (Live/VOD)
* Falha ao processar solicitação de manifesto ao vivo: URL da solicitação. (Ao vivo)
* Falha ao retornar um manifesto de variante: mensagem de erro.
* Falha ao validar ID de grupo: ID do grupo.
* Buscando manifesto bruto: URL do conteúdo. (Ao vivo)
* Após o redirecionamento VAST: URL de redirecionamento.
* Encontrado vazio disponível. (VOD)
* Encontrados *anúncios numéricos*. (VOD)
* Solicitação HTTP recebida. (Mensagem muito inicial)
* Ignorando anúncio porque a diferença entre a duração da resposta do anúncio (*duração da resposta do anúncio *s) e a duração real do anúncio (*duração real *s) é maior que o limite. (HLSManifestResolver)
* Ignorando o valor que não forneceu o valor da ID. (GroupAdResolver.java)
* Ignorando o valor válido que forneceu o valor de tempo inválido: *time *for availId = ID válida.
* Ignorando o valor válido que forneceu o valor de duração inválido: *duration *for availId = ID válida.
* Inicializar nova sessão. (Variante)
* Método HTTP inválido. Deve ser uma GET. (VOD)
* Método HTTP inválido. A solicitação de rastreamento deve ser um GET. (Ao vivo)
* Mensagem de erro de URL solicitado inválido. (Variante)
* Grupo inválido. (HLSManifestResolver)
* Solicitação inválida. Legenda não é uma solicitação de rastreamento válida. (VOD)
* Solicitação inválida. O pedido de legenda deve ser feito após o estabelecimento da sessão. (VOD)
* Solicitação inválida. A solicitação de rastreamento deve ser feita após o estabelecimento da sessão. (VOD)
* Instância de servidor inválida para ID de grupo de sobrecarga: ID do grupo. (Ao vivo)
* Limite de redirecionamentos VAST atingido - número.
* Fazer chamada de anúncio: URL de chamada de anúncio.
* Não foi encontrado nenhum manifesto para: URL do conteúdo. (Ao vivo)
* Nenhum valor correspondente encontrado para a ID válida: ID válida. (HLSManifestResolver)
* Nenhuma sessão de reprodução encontrada. (HLSManifestResolver)
* Processando solicitação VOD para URL de conteúdo manifesto.
* Variante de processamento.
* Solicitação de legenda de processamento para URL de conteúdo de manifesto.
* Processando solicitação de rastreamento. (VOD)
* Redirecionar resposta de anúncio vazia. (VASTStAX)
* Solicitação: URL.
* Resposta de erro de retorno para a solicitação do GET porque nenhuma sessão de reprodução foi encontrada. (VOD)
* Retornando resposta de erro para a solicitação GET devido a um erro interno do servidor.
* Resposta de erro de retorno para a solicitação do GET que especifica um ativo inválido: ID de solicitação de anúncio. (VOD)
* Resposta de erro de retorno para a solicitação do GET que especifica uma ID de grupo inválida ou vazia: ID do grupo. (VOD)
* Resposta de erro de retorno para a solicitação do GET que especifica um valor de posição de rastreamento inválido. (VOD)
* Resposta de erro de retorno para solicitação GET com sintaxe inválida - URL de solicitação. (Live/VOD)
* Resposta de erro de retorno para a solicitação com método HTTP não suportado: GET|POST. (Live/VOD)
* Retornando manifesto do cache. (VOD)
* O servidor está sobrecarregado. Continue sem a solicitação do ponto de anúncio. (Variante)
* Comece a gerar o manifesto direcionado. (HLSManifestResolver)
* Comece gerando manifesto de variante a partir de: URL do conteúdo. (Variante)
* Comece a compilar anúncios em manifesto. (VODHLSResolver)
* Tentando compilar anúncio em `HH:MM:SS`: AdPlacement \[adManifestURL= ad Manifest URL, durationSeconds= seconds, ignore= ignore, redirectAd= redirect ad, priority= priority.\] \(HLSManifestResolver\)
* Não é possível obter anúncios devido a uma linha de tempo inválida - retornou o conteúdo sem anúncios. (VOD)
* Não é possível obter anúncios - retornou o conteúdo sem anúncios. (VOD)
* Não é possível obter consulta de anúncio e nenhum URL de conteúdo foi fornecido. (VOD)
* URL válido recebido. (VOD/Variante)
* Variante M3U8 não encontrada. (Variante)

### TRACE_PLAYBACK_PROGRESS registra {#trace-playback-progress-records}

O servidor manifest gera registros desse tipo quando recebe um sinal sobre o progresso da reprodução durante o workflow de rastreamento do lado do servidor. Os campos além de `TRACE_PLAYBACK_PROGRESS` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código do status HTTP |
| largura de banda | integer | Largura de banda do fluxo |
| pts | integer | Tempo PTS no fluxo |
| ms_time | integer | Tempo quando o servidor de manifesto gerou o URL de rastreamento |
| url | string | Redirecionar URL |
| **¿** header_user_agent | string | Cabeçalho do agente do usuário HTTP |
| **¿** header_dnt | integer | Cabeçalho de não rastreamento HTTP |
| **Endereço_remoto_** efetivo | string | Endereço remoto efetivo IPv4 |
| **Endereço_** remoto | string | Endereço remoto IPv4 |

**-** Os últimos quatro campos são opcionais.

## Fluxos de taxa de bits múltipla {#multiple-bitrate-streams}

As solicitações do cliente para inserção de anúncio normalmente especificam mais de uma taxa de bits na lista de reprodução de variante formatada em M3U8. O servidor manifest gera e retorna um novo arquivo de variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Também gera uma ID de grupo exclusiva para unir esses M3U8s.

O servidor manifest usa as informações na solicitação do URL do Bootstrap do cliente para recuperar a lista de reprodução da variante de conteúdo. Ele gera uma nova lista de reprodução de variante contendo links de servidor de manifesto para o conteúdo no nível do fluxo. O cliente os usa para criar solicitações de inserção de anúncio. Os links de conteúdo no nível de fluxo do servidor de manifesto têm o seguinte formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vodO servidor de manifesto define este valor com base no tipo de lista de reprodução do conteúdo: Ao vivo/linear (
`#EXT-X-PLAYLIST-TYPE:EVENT`) ou VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* ****
ID exclusiva do publisherAssetIDPublisher para o conteúdo específico fornecido na solicitação de URL do Bootstrap.

* ****
renditionO servidor de manifesto define isso com base no 
`BANDWIDTH` do fluxo de conteúdo e o usa para corresponder a taxa de bits do anúncio à taxa de bits do conteúdo. A taxa de bits do anúncio não pode exceder a taxa de bits do conteúdo, a menos que a renderização do anúncio com a taxa de bits mais baixa o faça.

* ****
groupIDTo servidor de manifesto gera esse valor e o usa para garantir que adicione anúncios de forma consistente, independentemente de qual taxa de bits represente os anúncios do cliente.

* **url codificado em base64 do**
fluxo de taxa de bits. A base64 segura para URL do servidor de manifesto codifica o URL absoluto do fluxo de conteúdo. Cada fluxo tem seu próprio URL.

* **Parâmetros**
de consultaParâmetros de consulta fornecidos na solicitação de URL do Bootstrap.
