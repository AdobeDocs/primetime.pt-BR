---
title: Ferramenta de Depuração do Servidor Manifest
description: Ferramenta de Depuração do Servidor Manifest
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# Ferramenta de Depuração do Servidor Manifest {#manifest-server-debugging-tool}

A ferramenta de depuração permite que os editores investiguem problemas de inserção de anúncios potencialmente caros examinando informações de depuração retornadas em tempo real pelo servidor manifest em cabeçalhos HTTP ou, quando são necessárias informações mais detalhadas, examinando logs de sessão após o fato. Parceiros de Adobe, como o Akamai, podem usar a ferramenta para depurar suas integrações com o Primetime e o Decisioning.

A ferramenta oferece suporte à depuração de problemas de inserção de anúncios em qualquer uma das principais configurações de rastreamento de anúncios do servidor de manifesto:

* Rastreamento do lado do cliente com um reprodutor com base no TVSDK.
* Rastreamento do lado do cliente com um reprodutor não baseado no TVSDK.
* Rastreamento do lado do servidor.

Para oferecer suporte a todos esses casos, a ferramenta não exige ou usa códigos de editor do player.

Ao iniciar uma sessão de servidor de manifesto, você pode definir um parâmetro no URL da solicitação para solicitar que ele registre informações de depuração. Usando valores diferentes desse parâmetro, também é possível solicitar que o servidor de manifesto retorne informações de depuração especificadas em cabeçalhos HTTP, mas os cabeçalhos podem conter apenas uma quantidade limitada de informações. Você pode obter credenciais do Adobe para acessar arquivos de log completos, que o servidor de manifesto salva periodicamente (por exemplo, a cada hora) em um servidor de arquivamento. Depois de ter as credenciais para esse servidor, você poderá acessá-lo diretamente a qualquer momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opções da ferramenta Depuração {#debugging-tool-options}

Ao chamar a ferramenta de depuração, você tem várias opções para quais informações o servidor de manifesto retorna em cabeçalhos HTTP. As opções não afetam o que o servidor de manifesto coloca nos arquivos de log.

### Especificação de ptdebug {#specifying-ptdebug}

Ao iniciar o log de depuração para uma sessão do servidor de manifesto, você pode adicionar o parâmetro ptdebug ao URL da solicitação para especificar as seguintes opções para as informações que o servidor de manifesto retorna em cabeçalhos HTTP:

* ptdebug=true Todos os registros exceto `TRACE_HTTP_HEADER` e a maioria `call/response data` de `TRACE_AD_CALL` registros.
* ptdebug=AdCall Only TRACE_AD_*type* (por exemplo, TRACE_AD_CALL) registros.
* ptdebug=Header Somente registros TRACE_HTTP_HEADER.

As opções não afetam o que o servidor de manifesto coloca nos arquivos de log. Você não tem controle sobre isso, mas os arquivos de log são arquivos de texto, portanto, você pode aplicar uma grande variedade de ferramentas para extrair e reformatar as informações que lhe interessam.

Este é um exemplo do cabeçalho HTTP retornado quando `ptdebug=Header`. Algumas sequências longas de dígitos hexadecimais são substituídas por `. . .` para maior clareza.

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
| request_id | string | ID da solicitação usada pelo servidor de manifesto (carimbo de data e hora unix) |
| session_id | string | ID da sessão usada pelo servidor de manifesto |
| zone_id | inteiro | ID da Zona |
| record_type | string | Tipo de evento que está sendo registrado |
| outros campos | *** | Depende do tipo de evento |

### registros TRACE_REQUEST_INFO {#trace-request-info-records}

Registros desse tipo registram os resultados de solicitações HTTP. Os campos além de TRACE_REQUEST_INFO aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| método_solicitação | string | Método HTTP (GET ou POST) |
| request_uri | string | URI de solicitação HTTP (sem host) |
| request_length | inteiro | Comprimento da solicitação (bytes) |
| response_length | inteiro | Comprimento da resposta (bytes) |
| delta | inteiro | Tempo (milissegundos) para processar a solicitação |
| module_type | string | Variante, fluxo ou VOD |
| remote_address_aud_client_ip | string | (consulte a observação) |
| remote_address_x_fwd_for_hdr_key | string | (consulte a observação) |
| remote_host_port | string | (consulte a observação) |

>[!NOTE]
>
>Os três últimos campos são opcionais.

Um exemplo:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### registros TRACE_HTTP_HEADER {#trace-http-header-records}

Registros desse tipo registram cabeçalhos HTTP trocados durante chamadas HTTP entre o servidor de manifesto e o cliente, o servidor de publicidade ou o servidor de conteúdo. Os campos além de TRACE_HTTP_HEADER aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| request_type | string | Tipo de solicitação (MAIN ou UNKNOWN) |
| request_response | string | Cabeçalho de resposta (solicitação ou resposta) |
| header_name | string | Nome do cabeçalho HTTP |
| header_value | string | Valor do cabeçalho HTTP codificado na Base64 |

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

### registros TRACE_AD_CALL {#trace-ad-call-records}

Registros desse tipo registram os resultados das solicitações de anúncios do servidor de manifesto. Os campos além de TRACE_AD_CALL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| request_duration | inteiro | Tempo (em milissegundos) desde a solicitação até a resposta |
| ad_server_query_url | string | URL da chamada de publicidade, incluindo parâmetros de consulta |
| ad_system_id | string | Sistema de publicidade, da resposta do servidor de publicidade (Auditoria, se não especificado) |
| avail_id | string | ID da vantagem, da sugestão de anúncio no arquivo de manifesto de conteúdo (N/D para VOD) |
| avail_duration | número | Duração (segundos) da falha, a partir da sinalização de anúncio no arquivo de manifesto de conteúdo (N/D para VOD) |
| ad_server_response | string | Resposta codificada na base64 do servidor de publicidade |

Um exemplo:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### registros TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Os registros desse tipo registram os resultados das solicitações de publicidade indicadas pelo tipo de registro. Os campos além do tipo de registro aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| avail_id | string | ID da discagem, da sugestão de anúncio no arquivo de manifesto de conteúdo (online) ou do servidor de manifesto (VOD) |
| ad_type | string | Tipo de anúncio (DIRECT ou REDIRECT) |
| ad_duration | inteiro | Duração (segundos) do anúncio, da resposta do servidor de publicidade |
| ad_content_url | string | URL do arquivo de manifesto do anúncio, da resposta do servidor de publicidade |
| ad_content_url_atual | string | URL do arquivo de manifesto do anúncio inserido. Vazio para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de publicidade, da resposta do servidor de publicidade (Auditoria, se não especificado) |
| ad_id | string | ID do anúncio, da resposta do servidor de publicidade |
| creative_id | string | ID da ferramenta criativa, do nó de publicidade, da resposta do servidor de publicidade |
| ad_call_id | string | Não usado. Reservado para uso futuro. |
| delta | inteiro | Tempo (milissegundos) gasto por este evento |
| diversos | string | Motivo pelo qual o anúncio foi ignorado |

>[!NOTE]
>
>Os campos ad_content_url_atual, ad_call_id e misc são opcionais.

Para TRACE_AD_RESOLVE e TRACE_AD_INSERT, o URL no campo ad_content_url_atual é para o anúncio transcodificado, se houver um disponível. Caso contrário, o campo fica vazio para TRACE_AD_RESOLVE ou o mesmo que ad_content_url para TRACE_AD_INSERT.

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

### registros TRACE_TRACKING_URL {#trace-tracking-url-records}

Registros desse tipo registram os resultados das solicitações de anúncios do servidor de manifesto. Os campos além de TRACE_TRACKING_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| pts | número | Carimbo de data e hora do programa. Tempo no vídeo para chamar o URL. |
| ad_system | string | Sistema de publicidade (auditude ou freewheel) |
| url | string | URL com ping |
| status | string | Status HTTP retornado do ping |

Um exemplo:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registros {#trace-transcoding-no-media-to-transcode-records}

Os registros desse tipo registram um anúncio criativo ausente. O único campo além de TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE aparece na tabela.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| ad_id | string | ID de anúncio totalmente qualificado `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` PROTOCOLO: AUDITUDE, VAST) |

### TRACE_TRANSCODING_REQUESTED registros {#trace-transcoding-requested-records}

Registros desse tipo registram os resultados das solicitações de transcodificação que o servidor de manifesto envia para o CRS. Os campos além de TRACE_TRANSCODING_REQUESTED aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| ad_id | string | ID de anúncio totalmente qualificado |
| ad_manifest_url | string | URL do arquivo de manifesto do anúncio, da resposta do servidor de publicidade |
| creative_type | string | Tipo de mídia |
| sinalizadores | string | ID3 indica se a solicitação de transcodificação inclui uma solicitação para adicionar uma tag ID3 |
| target_duration | string | Duração alvo (segundos) do criativo transcodificado |

### registros TRACE_TRACKING_REQUEST {#trace-tracking-request-records}

Os registros desse tipo indicam uma solicitação para fazer o rastreamento no lado do servidor. Os campos além de TRACE_TRACKING_REQUEST aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| tracking_url_count | inteiro | Número de URLs de rastreamento |
| start | flutuante | Hora de início do fragmento PTS (segundos com precisão de milissegundos) |
| fim | flutuante | Hora de término do fragmento PTS (segundos com precisão de milissegundos) |

### registros TRACE_TRACKING_REQUEST_URL {#trace-tracking-request-url-records}

Os registros desse tipo fornecem um URL de rastreamento para rastreamento no lado do servidor. Os campos além de TRACE_TRACKING_REQUEST_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| carimbo de data e hora | flutuante | Tempo (segundos, com precisão .001) na sessão de reprodução para executar ping no URL de rastreamento |
| ad_system | string | Sistema de publicidade (por exemplo, auditude) |
| url | string | URL para ping |

### registros TRACE_WEBVTT_REQUEST {#trace-webvtt-request-records}

Registros desse tipo solicitam o servidor de manifesto para as legendas WEBVTT. Os campos além de TRACE_WEBVTT_REQUEST aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| vtt_uri | string | URL da solicitação |
| start | flutuante | Dividir hora de início (segundos com precisão de milissegundos) |
| fim | flutuante | Dividir hora de término (segundos com precisão de milissegundos) |

### registros TRACE_WEBVTT_RESPONSE {#trace-webvtt-response-records}

Registros ``of ``este ``type ``log ``responses ``o ``manifest ``server ``sends ``para ``clients ``in `` `answer` ``para ``requests `` `for` ``WEBVTT ``legendas. Os campos além de TRACE_WEBVTT_RESPONSE &quot;aparecem na ordem mostrada na tabela, separados `by`guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| resposta | string | Resposta codificada na Base64 enviada ao cliente |

### registros TRACE_WEBVTT_SOURCE {#trace-webvtt-source-records}

Registros desse tipo registram respostas de log a solicitações feitas pelo servidor de manifesto para legendas WEBVTT. Os campos além de TRACE_WEBVTT_SOURCE aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| origem | string | Conteúdo VTT original codificado na base64 |


### registros TRACE_MISC {#trace-misc-records}

Os registros desse tipo permitem que o servidor de manifesto registre eventos e informações não planejados quando assimila anúncios. O campo além de TRACE_MISC consiste em uma cadeia de caracteres de mensagem. As mensagens que podem aparecer incluem o seguinte:

* Anúncio ignorado: AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*segundos*, ignorar=*ignorar*, redirectAd=*redirectAd*, priority=*prioridade*
* O posicionamento do anúncio retornou como nulo.
* Anúncio compilado com sucesso.
* Falha na chamada de anúncio: *mensagem de erro*.
* Adicionando usuário-agente para buscar manifesto bruto: *user-agent*.
* Adicionando cookie para buscar manifesto bruto: [cookie]
* URL inválido *mensagem de erro de URL solicitado*. (Falha ao analisar o URL da variante)
* URL chamado: URL *obteve retorno: código de resposta*. ( URL ativo)
* URL chamado: URL *código de retorno: código de resposta*. (URL do VOD)
* Conflito encontrado ao resolver anúncios: o início da exibição intermediária ou o final da exibição intermediária está dentro do início da exibição ou do início da exibição antecipada contidos no VOD (mid-roll).
* Exceção sem tratamento detectada lançada pelo manipulador para URI: *URL da solicitação*.
* Geração de manifesto de variante concluída. (Variante)
* Geração de manifesto de variante concluída.
* Exceção ao manipular o redirecionamento VAST *URL de redirecionamento *erro: *mensagem de erro*.
* Falha ao obter a lista de reprodução do anúncio para *URL do manifesto de publicidade*.
* Falha ao gerar manifesto direcionado. (HLSManifestResolver)
* Falha ao analisar a primeira resposta da chamada de anúncio: *mensagem de erro*.
* Falha ao processar *GET|POST *solicitação para caminho: *URL da solicitação*. (Live/VOD)
* Falha ao processar solicitação de manifesto em tempo real: *URL da solicitação*. (Ao vivo)
* Falha ao retornar um manifesto de variante: *mensagem de erro*.
* Falha ao validar a ID do grupo: *ID do grupo*.
* Buscando manifesto bruto: *URL de conteúdo*. (Ao vivo)
* Após o redirecionamento VAST: *URL de redirecionamento*.
* Disponibilidade vazia encontrada. (VOD)
* *número *anúncios encontrados. (VOD)
* Solicitação HTTP recebida. (Primeira mensagem)
* Ignorando anúncio porque a diferença entre a duração da resposta do anúncio (*duração da resposta do anúncio *seg) e a duração real do anúncio (*duração real *seg) é maior que o limite. (HLSManifestResolver)
* Ignorando a disp que não forneceu nenhum valor de ID. (GroupAdResolver.java)
* Ignorando avail que forneceu valor de hora inválido: *hora *para availId = *ID disponível*.
* Ignorando valor de duração inválido fornecido por availId: *duração *para availId = *ID disponível*.
* Inicializar nova sessão. (Variante)
* Método HTTP inválido. Deve ser uma GET. (VOD)
* Método HTTP inválido. A solicitação de rastreamento deve ser uma GET. (Ao vivo)
* URL inválido *mensagem de erro de URL solicitado*. (Variante)
* Grupo inválido. (HLSManifestResolver)
* Solicitação inválida. A legenda não é uma solicitação de rastreamento válida. (VOD)
* Solicitação inválida. A solicitação de legenda deve ser feita após o estabelecimento da sessão. (VOD)
* Solicitação inválida. A solicitação de rastreamento deve ser feita após o estabelecimento da sessão. (VOD)
* Instância de servidor inválida para ID de grupo de sobrecarga: *ID do grupo*. (Ao vivo)
* Limite de redirecionamentos VAST atingido - *número*.
* Fazendo chamada de publicidade: *URL da chamada de publicidade*.
* Nenhum manifesto encontrado para: *URL de conteúdo*. (Ao vivo)
* Nenhuma ID disponível correspondente encontrada para: *ID disponível*. (HLSManifestResolver)
* Nenhuma sessão de reprodução encontrada. (HLSManifestResolver)
* Processando solicitação de VOD para manifesto *URL de conteúdo*.
* Variante de processamento.
* Processando solicitação de legenda para manifesto *URL de conteúdo*.
* Processando solicitação de rastreamento. (VOD)
* Resposta de publicidade de redirecionamento vazia. ( VASTStAX)
* Solicitando: *URL*.
* Retornando resposta de erro para a solicitação GET porque nenhuma sessão de reprodução foi encontrada. (VOD)
* Retornando resposta de erro para a solicitação GET devido a um erro interno do servidor.
* Retornando a resposta de erro para a solicitação GET que especifica um ativo inválido: *ID da solicitação de publicidade*. (VOD)
* Retornando a resposta de erro para a solicitação GET especificando uma ID de grupo inválida ou vazia: *ID do grupo*. (VOD)
* Retornando resposta de erro para a solicitação GET que especifica um valor de posição de rastreamento inválido. (VOD)
* Retornando resposta de erro para a solicitação GET com sintaxe inválida - *URL da solicitação*. (Live/VOD)
* Retornando a resposta de erro para a solicitação com o método HTTP não compatível: *GET|POST*. (Live/VOD)
* Retornando manifesto do cache. (VOD)
* Servidor sobrecarregado. Continue sem a solicitação de compilação de anúncio. (Variante)
* Iniciar geração de manifesto direcionado. (HLSManifestResolver)
* Começar a gerar manifesto de variante de: *URL de conteúdo*. (Variante)
* Comece a compilar anúncios no manifesto. (VODHLSResolver)
* Tentando compilar o anúncio em `HH:MM:SS`: AdPlacement \[adManifestURL=*URL do manifesto de publicidade*, durationSeconds=*segundos*, ignorar=*ignorar*, redirectAd=*redirecionar anúncio*, priority=*prioridade*.\]
* Não é possível obter anúncios devido a uma pttimeline inválida - o conteúdo retornou sem anúncios. (VOD)
* Não é possível obter anúncios. O conteúdo foi retornado sem anúncios. (VOD)
* Não é possível obter a consulta de publicidade e nenhum URL de conteúdo foi fornecido. (VOD)
* URL válido recebido. (VOD/variante)
* Variante M3U8 não encontrada. (Variante)

### registros TRACE_TRACKING_URL {#trace-tracking-url-records-1}

O servidor de manifesto gera registros desse tipo depois de chamar um URL de rastreamento durante o fluxo de trabalho de rastreamento do lado do servidor. Os campos além de TRACE_TRACKING_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| pts | número | Tempo de PTS dentro do fluxo |
| ad_system | string | Sistema de publicidade do anúncio (auditado ou freewheel) |
| url | string | URL com ping |
| state | string | Código de status HTTP |

### registros TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

O servidor de manifesto gera registros desse tipo quando recebe um sinal sobre o progresso da reprodução durante o fluxo de trabalho de rastreamento do lado do servidor. Os campos além de TRACE_PLAYBACK_PROGRESS aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP |
| largura de banda | inteiro | Largura de banda do fluxo |
| pts | inteiro | Tempo de PTS dentro do fluxo |
| ms_time | inteiro | Hora em que o servidor de manifesto gerou o URL de rastreamento |
| url | string | URL de redirecionamento |
| header_user_agent | string | cabeçalho User-Agent do HTTP |
| header_dnt | inteiro | Cabeçalho do-not-track do HTTP |
| effectiveness_remote_address | string | Endereço remoto efetivo IPv4 |
| remote_address | string | Endereço remoto IPv4 |

>[!NOTE]
>
>Os últimos quatro campos são opcionais.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
