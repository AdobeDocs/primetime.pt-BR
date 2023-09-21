---
title: Registro detalhado
description: Registro detalhado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---

# Registro detalhado {#verbose-logging}

## descrições de eventos ptdebug/logging {#ptdebug-logging-events}

Ao iniciar o log de depuração para uma sessão do servidor manifest, você pode adicionar o `ptdebug` parâmetro para o URL da solicitação para especificar as seguintes opções para as informações que o servidor de manifesto retorna em cabeçalhos HTTP:

* `ptdebug=true`
Todos os registros, exceto TRACE_HTTP_HEADER e a maioria dos dados de chamada/resposta dos registros TRACE_AD_CALL.

* `ptdebug=AdCall`
Somente registros do tipo TRACE_AD_ (por exemplo, TRACE_AD_CALL).

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
| zone_id | inteiro | Zona |
| record_type | string | Tipo de evento que está sendo registrado |
| outros campos | varia | Depende do tipo de evento |

Registros desse tipo registram os resultados de solicitações HTTP. Campos além `TRACE_REQUEST_INFO` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| método_solicitação | string | Método HTTP (GET ou POST) |
| request_uri | string | URI de solicitação HTTP (sem host) |
| request_length | inteiro | Comprimento da solicitação (bytes) |
| response_length | inteiro | Comprimento da resposta (bytes) |
| delta | inteiro | Tempo (milissegundos) para processar a solicitação |
| module_type | string | Variante, fluxo ou VOD |
| remote_address_aud_client_ip | string | **‡** |
| remote_address_x_fwd_for_hdr_key | string | **‡** |
| remote_host_port | string | **‡** |

**‡** Os três últimos campos são opcionais.

**Um exemplo**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### registros TRACE_HTTP_HEADER {#trace-http-header-records}

Registros desse tipo registram cabeçalhos HTTP trocados durante chamadas HTTP entre o servidor de manifesto e o cliente, o servidor de publicidade ou o servidor de conteúdo. Os campos além de TRACE_HTTP_HEADER aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| request_type | string | Tipo de solicitação (MAIN ou UNKNOWN) |
| request_response | string | Cabeçalho de resposta (solicitação ou resposta) |
| header_name | string | Nome do cabeçalho HTTP |
| header_value | string | Valor do cabeçalho HTTP codificado na Base64 |

>[!NOTE]
>
>A variável `request_type` e `header_value` Os campos são opcionais.

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

### registros TRACE_AD_CALL {#tracing-ad-call-records}

Registros desse tipo registram os resultados das solicitações de anúncios do servidor de manifesto. Campos além `TRACE_AD_CALL` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| request_duration | inteiro | Tempo (em milissegundos) desde a solicitação até a resposta |
| ad_server_query_url | string | URL da chamada de publicidade, incluindo parâmetros de consulta |
| ad_system_id | string | Sistema de publicidade, da resposta do servidor de publicidade (Auditude, se não especificado) |
| avail_id | string | ID da vantagem, da sugestão de anúncio no arquivo de manifesto de conteúdo (N/D para VOD) |
| avail_duration | número | Duração (segundos) da falha, a partir da sinalização de anúncio no arquivo de manifesto de conteúdo (N/D para VOD) |
| ad_server_response | string | Resposta codificada na base64 do servidor de publicidade |

Um exemplo:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### registros TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-resolve-redirect}

Os registros desse tipo registram os resultados das solicitações de publicidade indicadas pelo tipo de registro. Os campos além do tipo de registro aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado. |
| avail_id | string | ID da discagem, da sugestão de anúncio no arquivo de manifesto de conteúdo (online) ou do servidor de manifesto (VOD). |
| ad_type | string | Tipo de anúncio (DIRECT ou REDIRECT). |
| ad_duration | inteiro | Duração (segundos) do anúncio, da resposta do servidor de publicidade. |
| ad_content_url | string | URL do arquivo de manifesto do anúncio, da resposta do servidor de publicidade. |
| **†** ad_content_url_atual | string | URL do arquivo de manifesto do anúncio inserido. Vazio para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de publicidade, da resposta do servidor de publicidade (Auditude, se não especificado). |
| ad_id | string | ID do anúncio, da resposta do servidor de anúncios. |
| creative_id | string | ID da criação, do nó de publicidade, da resposta do servidor de publicidade. |
| **†** ad_call_id | string | Não usado. Reservado para uso futuro. |
| delta | inteiro | Tempo (milissegundos) gasto por esse evento. |
| **†** diversos | string | Motivo da interrupção do anúncio. |

**†** `ad_content_url_actual`, `ad_call_id`, e `misc` Os campos são opcionais.

>[!NOTE]
>
>Para `TRACE_AD_RESOLVE` e `TRACE_AD_INSERT`, o URL no `ad_content_url_actual` é para o anúncio transcodificado e, se disponível. Caso contrário, o campo ficará vazio por `TRACE_AD_RESOLVE` ou o mesmo que `ad_content_url` para `TRACE_AD_INSERT`.

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

Os registros desse tipo registram um anúncio criativo ausente. O único campo além `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` aparece na tabela.

| Campo | Tipo | Descrição |
|---|---|---|
| ad_id | string | ID de anúncio totalmente qualificado (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLO: AUDITUDE,VAST) |

Registros desse tipo registram os resultados das solicitações de transcodificação que o servidor de manifesto envia para o CRS. Campos além `TRACE_TRANSCODING_REQUESTED` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| ad_id | string | ID de anúncio totalmente qualificado |
| ad_manifest_url | string | URL do arquivo de manifesto do anúncio, da resposta do servidor de publicidade |
| creative_type | string | Tipo de mídia |
| sinalizadores | string | ID3 indica se a solicitação de transcodificação inclui uma solicitação para adicionar uma tag ID3 |
| target_duration | string | Duração alvo (segundos) do criativo transcodificado |

Os registros desse tipo indicam uma solicitação para fazer o rastreamento no lado do servidor. Campos além `TRACE_TRACKING_REQUEST` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| tracking_url_count | inteiro | Número de URLs de rastreamento |
| start | flutuante | Hora de início do fragmento PTS (segundos com precisão de milissegundos) |
| fim | flutuante | Hora de término do fragmento PTS (segundos com precisão de milissegundos) |

Os registros desse tipo fornecem um URL de rastreamento para rastreamento no lado do servidor. Campos além `TRACE_TRACKING_REQUEST_URL` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| carimbo de data e hora | flutuante | Tempo (segundos, com precisão .001) na sessão de reprodução para executar ping no URL de rastreamento. |
| ad_system | string | Sistema de publicidade (por exemplo, auditude) |
| url | string | URL para ping |

Registros desse tipo fazem solicitações de log para o servidor de manifesto `WEBVTT` legendas. Campos além `TRACE_WEBVTT_REQUEST` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| vtt_uri | string | URL da solicitação |
| start | flutuante | Dividir hora de início (segundos com precisão de milissegundos) |
| fim | flutuante | Dividir hora de término (segundos com precisão de milissegundos) |

Registros desse tipo: respostas de log que o servidor de manifesto envia aos clientes em `answer` a pedidos de `WEBVTT` legendas. Campos além `TRACE_WEBVTT_RESPONSE` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| resposta | string | Resposta codificada na Base64 enviada ao cliente |

Registros desse tipo registram respostas de log a solicitações feitas pelo servidor de manifesto `WEBVTT` legendas. Campos além `TRACE_WEBVTT_SOURCE` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP retornado |
| origem | string | Conteúdo VTT original codificado na base64 |

Os registros desse tipo permitem que o servidor de manifesto registre eventos e informações não planejados quando assimila anúncios. O campo além `TRACE_MISC` consiste em uma cadeia de caracteres de mensagem. As mensagens que podem aparecer incluem o seguinte:

* Anúncio ignorado: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= segundos, ignorar= ignorar, redirectAd= redirectAd, priority= priority
* O posicionamento do anúncio retornou como nulo.
* Anúncio compilado com sucesso.
* Falha na chamada de anúncio : mensagem de erro.
* Adicionando usuário-agente para buscar manifesto bruto: user-agent.
* Adicionando cookie para buscar manifesto bruto: #
* Mensagem de erro de URL solicitado inválido. (Falha ao analisar o URL da variante)
* URL chamado: o URL obteve retorno: código de resposta. ( URL ativo)
* URL chamado: código de retorno do URL: código de resposta. (URL do VOD)
* Conflito encontrado ao resolver anúncios: o início da exibição intermediária ou o final da exibição intermediária está dentro do início da exibição ou do início da exibição antecipada contidos no VOD (mid-roll).
* Exceção sem tratamento detectada lançada pelo manipulador para URI: URL de solicitação.
* Geração de manifesto de variante concluída. (Variante)
* Geração de manifesto de variante concluída.
* Exceção ao manipular o redirecionamento VAST *URL de redirecionamento *erro: mensagem de erro.
* Falha ao obter a lista de reprodução do anúncio para o URL do manifesto do anúncio.
* Falha ao gerar manifesto direcionado. (HLSManifestResolver)
* Falha ao analisar a primeira resposta da chamada de anúncio: mensagem de erro.
* Falha ao processar *GET|POST *solicitação para caminho: URL de solicitação. (Live/VOD)
* Falha ao processar solicitação de manifesto ao vivo: URL da solicitação. (Ao vivo)
* Falha ao retornar um manifesto de variante: mensagem de erro.
* Falha ao validar a ID do grupo: ID do grupo.
* Buscando manifesto bruto: URL de conteúdo. (Ao vivo)
* Seguinte redirecionamento VAST: URL de redirecionamento.
* Disponibilidade vazia encontrada. (VOD)
* Encontrado *número* anúncios. (VOD)
* Solicitação HTTP recebida. (Primeira mensagem)
* Ignorando anúncio porque a diferença entre a duração da resposta do anúncio (*duração da resposta do anúncio *seg) e a duração real do anúncio (*duração real *seg) é maior que o limite. (HLSManifestResolver)
* Ignorando a disp que não forneceu nenhum valor de ID. (GroupAdResolver.java)
* Ignorando avail que forneceu valor de hora inválido: *time *para availId = avail ID.
* Ignorando valor de duração inválido fornecido: *duration *para availId = avail ID.
* Inicializar nova sessão. (Variante)
* Método HTTP inválido. Deve ser uma GET. (VOD)
* Método HTTP inválido. A solicitação de rastreamento deve ser uma GET. (Ao vivo)
* Mensagem de erro de URL inválido solicitado. (Variante)
* Grupo inválido. (HLSManifestResolver)
* Solicitação inválida. A legenda não é uma solicitação de rastreamento válida. (VOD)
* Solicitação inválida. A solicitação de legenda deve ser feita após o estabelecimento da sessão. (VOD)
* Solicitação inválida. A solicitação de rastreamento deve ser feita após o estabelecimento da sessão. (VOD)
* Instância de servidor inválida para ID de grupo de sobrecarga: ID de grupo. (Ao vivo)
* Limite de redirecionamentos VAST atingido - número.
* Fazendo chamada de anúncio: URL da chamada de anúncio.
* Nenhum manifesto encontrado para: URL de conteúdo. (Ao vivo)
* Nenhuma correspondência disponível encontrada para ID disponível: ID disponível. (HLSManifestResolver)
* Nenhuma sessão de reprodução encontrada. (HLSManifestResolver)
* Processando solicitação de VOD para URL de conteúdo de manifesto.
* Variante de processamento.
* Processando solicitação de legenda para URL de conteúdo de manifesto.
* Processando solicitação de rastreamento. (VOD)
* Resposta de publicidade de redirecionamento vazia. ( VASTStAX)
* Solicitando: URL.
* Retornando resposta de erro para a solicitação GET porque nenhuma sessão de reprodução foi encontrada. (VOD)
* Retornando resposta de erro para a solicitação GET devido a um erro interno do servidor.
* Retornando a resposta de erro para a solicitação do GET que especifica um ativo inválido: ID da solicitação de anúncio. (VOD)
* Retornando resposta de erro para a solicitação GET especificando uma ID de grupo inválida ou vazia: ID de grupo. (VOD)
* Retornando resposta de erro para a solicitação GET que especifica um valor de posição de rastreamento inválido. (VOD)
* Retornando resposta de erro para a solicitação do GET com sintaxe inválida - URL da solicitação. (Live/VOD)
* Retornando a resposta de erro para a solicitação com o método HTTP não compatível: GET|POST. (Live/VOD)
* Retornando manifesto do cache. (VOD)
* Servidor sobrecarregado. Continue sem a solicitação de compilação de anúncio. (Variante)
* Iniciar geração de manifesto direcionado. (HLSManifestResolver)
* Comece a gerar o manifesto de variante a partir de: URL de conteúdo. (Variante)
* Comece a compilar anúncios no manifesto. (VODHLSResolver)
* Tentando compilar o anúncio em `HH:MM:SS`: AdPlacement \[adManifestURL= URL do manifesto do anúncio, durationSeconds= segundos, ignorar= ignorar, redirecionarAd= anúncio de redirecionamento, prioridade= prioridade.\] \(HLSManifestResolver\)
* Não é possível obter anúncios devido a uma pttimeline inválida - o conteúdo retornou sem anúncios. (VOD)
* Não é possível obter anúncios. O conteúdo foi retornado sem anúncios. (VOD)
* Não é possível obter a consulta de publicidade e nenhum URL de conteúdo foi fornecido. (VOD)
* URL válido recebido. (VOD/variante)
* Variante M3U8 não encontrada. (Variante)

### registros TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

O servidor de manifesto gera registros desse tipo quando recebe um sinal sobre o progresso da reprodução durante o fluxo de trabalho de rastreamento do lado do servidor. Campos além `TRACE_PLAYBACK_PROGRESS` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|---|---|---|
| status | string | Código de status HTTP |
| largura de banda | inteiro | Largura de banda do fluxo |
| pts | inteiro | Tempo de PTS dentro do fluxo |
| ms_time | inteiro | Hora em que o servidor de manifesto gerou o URL de rastreamento |
| url | string | URL de redirecionamento |
| **0** header_user_agent | string | cabeçalho User-Agent do HTTP |
| **0** header_dnt | inteiro | Cabeçalho do-not-track do HTTP |
| **0** effectiveness_remote_address | string | Endereço remoto efetivo IPv4 |
| **0** remote_address | string | Endereço remoto IPv4 |

**0** Os últimos quatro campos são opcionais.

## Vários fluxos de taxa de bits {#multiple-bitrate-streams}

As solicitações do cliente para inserção de anúncio normalmente especificam mais de uma taxa de bits na lista de reprodução formatada M3U8 da variante. O servidor de manifesto gera e retorna um novo arquivo variante M3U8 contendo um link M3U8 separado para cada taxa de bits. Ele também gera um identificador de grupo exclusivo para unir esses M3U8s.

O servidor de manifesto usa as informações na solicitação de URL do Bootstrap do cliente para recuperar a lista de reprodução de variantes de conteúdo. Ele gera uma nova lista de reprodução variante contendo links de servidor manifest para o conteúdo em nível de fluxo. O cliente os usa para criar solicitações de inserção de anúncios. Os links de conteúdo no nível do fluxo do servidor de manifesto têm o seguinte formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/vod**
O servidor de manifesto define esse valor com base no tipo de playlist do conteúdo: Live/linear (`#EXT-X-PLAYLIST-TYPE:EVENT`) ou VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetID**
Identificador exclusivo do editor para o conteúdo específico fornecido na solicitação de URL do Bootstrap.

* **representação**
O servidor de manifesto define isso com base na variável `BANDWIDTH` do fluxo de conteúdo e o utiliza para corresponder a taxa de bits do anúncio à taxa de bits do conteúdo. A taxa de bits de anúncio não pode exceder a taxa de bits do conteúdo, a menos que a representação de anúncio com a taxa de bits mais baixa o faça.

* **groupID**
O servidor de manifesto gera esse valor e o usa para garantir que ele insira anúncios de forma consistente, independentemente da taxa de bits das representações que o cliente solicita.

* **url codificado em base64 do fluxo de taxa de bits**
A base64 segura para URL do servidor de manifesto codifica a URL absoluta do fluxo de conteúdo. Cada fluxo tem seu próprio URL.

* **Parâmetros de consulta**
Parâmetros de consulta fornecidos na solicitação de URL do Bootstrap.
