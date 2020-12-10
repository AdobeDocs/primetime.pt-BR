---
title: Ferramenta de depuração do servidor manifest
seo-title: Ferramenta de depuração do servidor manifest
description: Ferramenta de depuração do servidor manifest
seo-description: Ferramenta de depuração do servidor manifest
uuid: 0b4f06f5-4b1f-4f88-980a-5b4df28e0094
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiquuid: 00b49659-ce56-4b5c-87cd-c357a0936641
donotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: 3efbd1113e82c4d5f84798997b6f744daf6f508e
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 0%

---


# Ferramenta de depuração do servidor manifest {#manifest-server-debugging-tool}

## Visão geral da ferramenta de depuração {#overview-of-debugging-tool}

A ferramenta de depuração permite que os editores investiguem problemas de inserção de anúncios potencialmente caros examinando as informações de depuração retornadas em tempo real pelo servidor manifest nos cabeçalhos HTTP ou, quando informações mais detalhadas forem necessárias, examinando os logs da sessão após o fato. Parceiros Adobe como o Akamai podem usar a ferramenta para depurar suas integrações com a decisão do anúncio Primetime.

A ferramenta oferece suporte à depuração de problemas de inserção em qualquer uma das configurações principais de rastreamento de anúncios do servidor manifest:

* Rastreamento do lado do cliente com um player com base no TVSDK.
* Rastreamento do lado do cliente com um player não baseado no TVSDK.
* Rastreamento do lado do servidor.

Para suportar todos esses casos, a ferramenta não exige nem usa códigos de editor do player.

Ao iniciar uma sessão do servidor manifest, você pode definir um parâmetro no URL da solicitação para solicitar que ele registre informações de depuração. Usando valores diferentes desse parâmetro, também é possível solicitar ao servidor manifest que retorne partes específicas das informações de depuração em cabeçalhos HTTP, mas os cabeçalhos podem conter apenas uma quantidade limitada de informações. Você pode obter credenciais do Adobe para acessar arquivos de log completos, que o servidor manifest salva periodicamente (por exemplo, de hora em hora) em um servidor de arquivamento. Depois de ter credenciais para esse servidor, você poderá acessá-lo diretamente a qualquer momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opções da ferramenta de depuração {#debugging-tool-options}

Ao chamar a ferramenta de depuração, você tem várias opções para quais informações o servidor manifest retorna nos cabeçalhos HTTP. As opções não afetam o que o servidor manifest posiciona nos arquivos de log.

### Especificação de ptdebug {#specifying-ptdebug}

Ao iniciar o registro de depuração para uma sessão do servidor manifest, você pode adicionar o parâmetro ptdebug ao URL da solicitação para especificar as seguintes opções para as informações que o servidor manifest retorna nos cabeçalhos HTTP:

* ptdebug=true Todos os registros, exceto `TRACE_HTTP_HEADER` e a maioria `call/response data` dos registros `TRACE_AD_CALL`.
* ptdebug=AdCall Somente registros TRACE_AD_*type* (por exemplo, TRACE_AD_CALL).
* ptdebug=Somente cabeçalho registros TRACE_HTTP_HEADER.

As opções não afetam o que o servidor manifest posiciona nos arquivos de log. Você não tem controle sobre isso, mas os arquivos de registro são arquivos de texto, portanto, você pode aplicar uma grande variedade de ferramentas para extrair e reformatar as informações que lhe interessam.

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
| request_id | string | ID da solicitação usada pelo servidor manifest (carimbo de data e hora único) |
| session_id | string | ID da sessão usada pelo servidor manifest |
| zone_id | integer | ID da zona |
| record_type | string | Tipo de evento que está sendo registrado |
| outros campos | *** | Depende do tipo de evento |

### TRACE_REQUEST_INFO registra {#trace-request-info-records}

Os registros deste tipo registram os resultados das solicitações HTTP. Os campos além de TRACE_REQUEST_INFO aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| request_method | string | Método HTTP (GET ou POST) |
| request_uri | string | URI de solicitação HTTP (sem host) |
| request_length | integer | Duração da solicitação (bytes) |
| response_length | integer | Duração da resposta (bytes) |
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

Registros desse tipo de cabeçalhos HTTP de log trocados durante chamadas HTTP entre o servidor do manifesto e o cliente, o servidor de publicidade ou o servidor de conteúdo. Os campos além de TRACE_HTTP_HEADER aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| request_type | string | Tipo de solicitação (MAIN ou UNKNOWN) |
| request_response | string | Cabeçalho de resposta (solicitação ou resposta) |
| nome_do_cabeçalho | string | Nome do cabeçalho HTTP |
| header_value | string | Valor do cabeçalho HTTP codificado em base64 |

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

Registros desse tipo registram os resultados de solicitações de anúncios do servidor manifest. Os campos além de TRACE_AD_CALL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| request_duration | integer | Tempo (milissegundos) da solicitação para a resposta |
| ad_server_query_url | string | URL para a chamada de anúncio, incluindo parâmetros de query |
| ad_system_id | string | Sistema de anúncio, da resposta do servidor de anúncio (Auditude se não especificado) |
| avail_id | string | ID do valor disponível, a partir da indicação de anúncio no arquivo manifest de conteúdo (N/A para VOD) |
| avail_duration | número | Duração (segundos) do recurso, a partir da indicação de anúncio no arquivo de manifesto do conteúdo (N/A para VOD) |
| ad_server_response | string | Resposta codificada em base64 do servidor de anúncios |

Um exemplo:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE e registros TRACE_AD_REDIRECT {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Registros desse tipo registram os resultados das solicitações de anúncio indicadas pelo tipo de registro. Os campos além do tipo de registro aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| avail_id | string | ID do disponível, da sinalização do anúncio no arquivo manifest do conteúdo (live) ou do servidor manifest (VOD) |
| ad_type | string | Tipo de anúncio (DIRECT ou REDIRECT) |
| ad_duration | integer | Duração (segundos) do anúncio, da resposta do servidor de anúncio |
| ad_content_url | string | URL do arquivo manifest do anúncio, a partir da resposta do servidor de publicidade |
| ad_content_url_atual | string | URL do arquivo manifest da publicidade inserida. Vazio para TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema de anúncio, da resposta do servidor de anúncio (Auditude se não especificado) |
| ad_id | string | ID do anúncio, da resposta do servidor de publicidade |
| creative_id | string | ID do anúncio, do nó do anúncio, da resposta do servidor de anúncios |
| ad_call_id | string | Não usado. Reservado para uso futuro. |
| delta | integer | Tempo (milissegundos) utilizado por este evento |
| misc | string | Motivo pelo qual o anúncio foi ignorado |

>[!NOTE]
>
>Os campos ad_content_url_atual, ad_call_id e diversos são opcionais.

Para TRACE_AD_RESOLVE e TRACE_AD_INSERT, o URL no campo ad_content_url_real é para o anúncio transcodificado, se disponível. Caso contrário, o campo estará vazio para TRACE_AD_RESOLVE ou o mesmo como ad_content_url para TRACE_AD_INSERT.

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

### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Registros desse tipo registram os resultados de solicitações de anúncios do servidor manifest. Os campos além de TRACE_TRACKING_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| pts | número | Carimbo de data e hora do programa. Tempo no vídeo para chamar o URL. |
| ad_system | string | Sistema publicitário (auditude ou roda livre) |
| url | string | URL com ping |
| status | string | Status HTTP retornado pelo ping |

Um exemplo:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE registros {#trace-transcoding-no-media-to-transcode-records}

Registros desse tipo registram uma publicidade criativa ausente. O único campo além de TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE aparece na tabela.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| ad_id | string | ID de anúncio totalmente qualificado `(FQ_AD_ID: Q_AD_ID[;Q_AD_ID[;Q_AD_ID...]]` Q_AD_ID: PROTOCOLO `PROTOCOL:AD_SYSTEM:AD_ID[:CREATIVE_ID[:MEDIA_ID]]`: AUDITUDE,VAST`)` |

### TRACE_TRANSCODING_REQUESTED registros {#trace-transcoding-requested-records}

Registros desse tipo registram os resultados das solicitações de transcodificação que o servidor manifest envia para o CRS. Os campos além de TRACE_TRANSCODING_REQUESTED aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| ad_id | string | ID de anúncio totalmente qualificado |
| ad_manifest_url | string | URL do arquivo manifest do anúncio, a partir da resposta do servidor de publicidade |
| creative_type | string | Tipo de mídia |
| sinalizadores | string | ID3 indica se a solicitação de transcodificação inclui uma solicitação para adicionar uma tag ID3 |
| público alvo_duration | string | Duração do público alvo (segundos) do anúncio transcodificado |

### TRACE_TRACKING_REQUEST registra {#trace-tracking-request-records}

Registros desse tipo indicam uma solicitação para fazer o rastreamento do lado do servidor. Os campos além de TRACE_TRACKING_REQUEST aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| tracking_url_count | integer | Número de URLs de rastreamento |
| start | flutuante | Tempo de start do fragmento PTS (segundos com precisão de milissegundos) |
| end | flutuante | Tempo de término do fragmento PTS (segundos com precisão de milissegundos) |

### TRACE_TRACKING_REQUEST_URL registra {#trace-tracking-request-url-records}

Os registros deste tipo fornecem um URL de rastreamento para o rastreamento do lado do servidor. Os campos além de TRACE_TRACKING_REQUEST_URL são exibidos na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| timestamp | flutuante | Tempo (segundos, com precisão .001) na sessão de reprodução para executar ping no URL de rastreamento |
| ad_system | string | Sistema de publicidade (por exemplo, auditude) |
| url | string | URL para ping |

### TRACE_WEBVTT_REQUEST registra {#trace-webvtt-request-records}

Registros desse tipo de solicitações de log feitas pelo servidor manifest para legendas WEBVTT. Os campos além de TRACE_WEBVTT_REQUEST aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| vtt_uri | string | URL para solicitação |
| start | flutuante | Dividir tempo de start (segundos com precisão de milissegundos) |
| end | flutuante | Tempo de término dividido (segundos com precisão de milissegundos) |

### TRACE_WEBVTT_RESPONSE registra {#trace-webvtt-response-records}

Registros desse tipo de respostas de log que o servidor manifest envia aos clientes em resposta a solicitações de legendas `WEBVTT`. Os campos além de `TRACE_WEBVTT_RESPONSE` aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| resposta | string | Resposta codificada em base64 enviada ao cliente |

### TRACE_WEBVTT_SOURCE registra {#trace-webvtt-source-records}

Registros desse tipo de respostas de log para solicitações feitas pelo servidor manifest para legendas WEBVTT. Os campos além de TRACE_WEBVTT_SOURCE são exibidos na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP retornado |
| fonte | string | Conteúdo VTT original codificado em base64 |


### TRACE_MISC registra {#trace-misc-records}

Registros desse tipo permitem que o servidor manifest registre eventos e informações não planejadas de outra forma quando ele ingere anúncios. O campo além de TRACE_MISC consiste em uma string de mensagem. As mensagens que podem aparecer incluem:

* Anúncio ignorado: AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*segundos*, ignore=*ignore*, redirectAd=*redirectAd*, priority=*priority*
* O posicionamento do anúncio retornou nulo.
* Anúncio costurado com êxito.
* Falha na chamada de anúncio: *mensagem de erro*.
* Adicionando Agente de Usuário para buscar o manifesto bruto: *user-agent*.
* Adicionar cookie para buscar o manifesto bruto: [cookie]
* URL inválido *mensagem de erro de URL solicitada*. (Falha ao analisar o URL variante)
* URL chamado: URL *tem retorno: código de resposta*. (Live URL)
* URL chamado: URL *código de retorno: código de resposta*. (URL VOD)
* Conflito encontrado ao resolver anúncios: quer um dos start médios ou médios, quer um dos valores médios normais, quer um dos valores anteriores à rolagem, quer um dos valores anteriores à rolagem (VOD).
* Exceção sem tratamento detectada emitida pelo manipulador para URI: *solicitação URL*.
* Geração de manifesto de variante concluída. (Variante)
* Geração de manifesto de variante concluída.
* Exceção ao manipular o redirecionamento VAST *URL de redirecionamento *erro: *mensagem de erro*.
* Falha ao obter a lista de reprodução do anúncio para *URL do manifesto do anúncio*.
* Falha ao gerar manifesto direcionado. (HLSManifestResolver)
* Falha ao analisar a primeira resposta de chamada de anúncio: *mensagem de erro*.
* Falha ao processar *GET|POST *solicitação para caminho: *solicitação URL*. (Ao vivo/VOD)
* Falha ao processar a solicitação de manifesto ao vivo: *solicitação URL*. (Ao vivo)
* Falha ao retornar um manifesto de variante: *mensagem de erro*.
* Falha ao validar a ID de grupo: *ID de grupo*.
* Buscando manifesto bruto: *URL de conteúdo*. (Ao vivo)
* Após o redirecionamento VAST: *redirecionar URL*.
* Encontrado vazio disponível. (VOD)
* Encontrado *número *anúncios. (VOD)
* Solicitação HTTP recebida. (Primeira mensagem)
* Ignorando anúncio porque a diferença entre a duração da resposta do anúncio (*duração da resposta do anúncio *s) e a duração do anúncio real (*duração real *s) é maior que o limite. (HLSManifestResolver)
* Ignorando o valor que não forneceu nenhum valor de ID. (GroupAdResolver.java)
* Ignorando o valor de tempo inválido fornecido: *time *for availId = *ID disponível*.
* Ignorando o valor de duração inválido fornecido: *duração *para availId = *ID disponível*.
* Inicializar nova sessão. (Variante)
* Método HTTP inválido. Deve ser uma GET. (VOD)
* Método HTTP inválido. A solicitação de rastreamento deve ser um GET. (Ao vivo)
* URL inválido *mensagem de erro de URL solicitada*. (Variante)
* Grupo inválido. (HLSManifestResolver)
* Solicitação inválida. Legenda não é uma solicitação de rastreamento válida. (VOD)
* Solicitação inválida. A solicitação de legenda deve ser feita após a sessão ser estabelecida. (VOD)
* Solicitação inválida. A solicitação de rastreamento deve ser feita após a sessão ser estabelecida. (VOD)
* Instância de servidor inválida para ID de grupo de sobrecarga: *ID de grupo*. (Ao vivo)
* Limite de redirecionamentos VAST atingido - *number*.
* Efetuando chamada de anúncio: *anúncio URL*.
* Nenhum manifesto encontrado para: *URL de conteúdo*. (Ao vivo)
* Não foi encontrado nenhum valor correspondente para a ID disponível: *ID disponível*. (HLSManifestResolver)
* Nenhuma sessão de reprodução encontrada. (HLSManifestResolver)
* Processando solicitação VOD para o manifesto *URL de conteúdo*.
* Variante de processamento.
* Processando solicitação de legenda para o manifesto *URL de conteúdo*.
* Processando solicitação de rastreamento. (VOD)
* Redirecionar resposta de anúncio vazia. (VASTStAX)
* Solicitando: *URL*.
* Retornando resposta de erro para solicitação de GET porque nenhuma sessão de reprodução foi encontrada. (VOD)
* Retornando resposta de erro para solicitação de GET devido a um erro interno do servidor.
* Retornando resposta de erro para solicitação de GET especificando um ativo inválido: *ID de solicitação de anúncio*. (VOD)
* Retornando resposta de erro para solicitação de GET especificando uma ID de grupo inválida ou vazia: *ID de grupo*. (VOD)
* Resposta de erro de retorno para solicitação de GET que especifica um valor de posição de rastreamento inválido. (VOD)
* Retornando resposta de erro para solicitação de GET com sintaxe inválida - *solicitação URL*. (Ao vivo/VOD)
* Retornando resposta de erro para solicitação com método HTTP não suportado: *GET|POST*. (Ao vivo/VOD)
* Retornando manifesto do cache. (VOD)
* O servidor está sobrecarregado. Continue sem solicitação de ponto de anúncio. (Variante)
* Start que gera manifesto direcionado. (HLSManifestResolver)
* Manifesto de variante de geração de start de: *URL de conteúdo*. (Variante)
* Start costurando publicidades em manifesto. (VODHLSResolver)
* Tentando unir anúncio em *HH:MM:SS*: AdPlacement adManifestURL=*ad Manifest URL*, durationSeconds=*segundos*, ignore=*ignore*, redirectAd=*redirecionar ad*, priority=*priority* ... (HLSManifestResolver)
* Não é possível obter anúncios devido a uma linha de tempo inválida - retornou o conteúdo sem anúncios. (VOD)
* Não é possível obter anúncios: retornou o conteúdo sem anúncios. (VOD)
* Não é possível obter o query do anúncio e nenhum URL de conteúdo foi fornecido. (VOD)
* URL válido recebido. (VOD/Variant)
* Variante M3U8 não encontrada. (Variante)

### TRACE_TRACKING_URL records {#trace-tracking-url-records-1}

O servidor manifest gera registros desse tipo depois de chamar um URL de rastreamento durante o fluxo de trabalho de rastreamento do lado do servidor. Os campos além de TRACE_TRACKING_URL aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| pts | número | Tempo PTS no fluxo |
| ad_system | string | Sistema de anúncios (auditude ou roda livre) |
| url | string | URL com ping |
| estado | string | Código de status HTTP |

### TRACE_PLAYBACK_PROGRESS registra {#trace-playback-progress-records}

O servidor manifest gera registros desse tipo quando recebe um sinal sobre o progresso da reprodução durante o fluxo de trabalho de rastreamento do lado do servidor. Os campos além de TRACE_PLAYBACK_PROGRESS aparecem na ordem mostrada na tabela, separados por guias.

| Campo | Tipo | Descrição |
|--- |--- |--- |
| status | string | Código de status HTTP |
| largura | integer | Largura de banda do fluxo |
| pts | integer | Tempo PTS no fluxo |
| ms_time | integer | Hora em que o servidor manifest gerou o URL de rastreamento |
| url | string | Redirecionar URL |
| header_user_agent | string | cabeçalho HTTP User-Agent |
| header_dnt | integer | Cabeçalho de não rastreamento HTTP |
| effective_remote_address | string | Endereço remoto efetivo IPv4 |
| remote_address | string | Endereço remoto IPv4 |

>[!NOTE]
>
>Os últimos quatro campos são opcionais.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte da Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
