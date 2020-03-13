---
description: Os parâmetros de consulta informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.
seo-description: Os parâmetros de consulta informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.
seo-title: Parâmetros de consulta do servidor manifest
title: Parâmetros de consulta do servidor manifest
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Parâmetros de consulta do servidor manifest {#manifest-server-query-parameters}

Os parâmetros de consulta informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.

O URL completo consiste no URL básico seguido de um ponto de interrogação e, em seguida, de `parameterName=value` argumentos, separados por E: `Base URL?name1=value1&name2=value2& . . .&name n=value n`

## Parâmetros reconhecidos {#section_072845B7FA94468C8068E9092983C9E6}

O servidor manifest reconhece os seguintes parâmetros. Processa-os ou os transmite, juntamente com todos os parâmetros não reconhecidos, para o servidor de anúncios.

| Principal | Descrição | Obrigatório | Valores Válidos |
|--- |--- |--- |--- |
| `__sid__` | ID exclusiva que o servidor manifest usa para gerar a ID da sessão. | Sim | Alfanumérico |
| g | Tipo de dispositivo cliente | Quando as regras de definição de metas dependem do tipo de dispositivo | Consulte a lista em Tipos [de](https://adobeprimetime.zendesk.com) clientes (requer acesso ao Zendesk) |
| k | Palavras-chave para direcionamento de anúncio personalizado | Não | Sequência segura para URL no formato key1=value1;key2=value2;. . . |
| u | ID do ativo de inserção do anúncio Primetime. | Sim | Valor de hash MD5 |
| z | Primetime e ID de Zona de inserção do ativo. | Sim | Número inteiro |
| enableC3 | O cliente está em uma janela C3. Se verdadeiro, substitua apenas os valores locais; caso contrário, substitua todos os disponíveis. | Não | Booleano |
| live | Indica se o conteúdo é um fluxo ao vivo ou VOD (vídeo sob demanda). | Cliente Akamai Ad Scaler ou iOS Safari | Booleano |
| pabimode | [Habilitar suporte para inserção](../../msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) parcial de anúncio Ativar se verdadeiro ou iniciar Desabilitar se falso | Não (o padrão está desativado) | start , true ou false |
| plataforma | Duração (segundos) da janela de identificação do anúncio: até que ponto procurar anúncios quando um usuário de DVR ingressar no stream. | Não (padrão = 1800) | 0 a 1800 |
| ptassetid | ID exclusiva do conteúdo atribuído e mantido pelo editor. | Akamai Ad Scaler | Sequência segura para URL |
| ptcdn | Lista de um ou mais CDNs para hospedar ativos transcodificados. Consulte Suporte a [vários CDN](../../creative-repackaging-service/multi-cdn-supportt.md). | Não (padrão=Akamai) | Exemplo: Akamai, Level3, Limelight, Comcast |
| ptcueformat | O nome do formato de sinalização de anúncio personalizado presente no M3U8. | Não | DPISimple, DPIScte35, Elemental, NBC, NFL ou Turner |
| failover de canal | Sinaliza o servidor de manifesto para identificar fluxos primários e de failover especificados na lista de reprodução mestre e para tratá-los como conjuntos de disjunção. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS.) Consulte [Facilitando a alternância](../../msapi-topics/ms-insert-ads/hls-switching-to-failover.md) do player HLS. | Não | true |
| tímulo | Se definido como true , várias chamadas publicitárias do Auditude para FER serão feitas; uma para cada pausa de anúncio.  Se ausente ou definido como falso, uma chamada publicitária é feita para auditude para FER. | Não | Nota Booleana:  Os seguintes requisitos: <ul><li>o parâmetro ptcueformat deve ser definido como nbc</li><li>o parâmetro da linha do tempo é ignorado.</li></ul> |
| jogador | Jogador que faz a solicitação. | iOS/Safari | ios-mobileweb |
| tendência | Gerado automaticamente por inserção de anúncio e usado pelo Akamai. Não adicione nem remova. | Akamai Ad Scaler |  |
| pttagds | Ativar tags [EXT-X- DISCONTINUITY- SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | Não | true - o servidor manifest inclui uma tag de sequência antes do conteúdo de cada arquivo m3u8 que enviar; se o parâmetro não estiver presente ou não for verdadeiro, o servidor manifest não incluirá uma tag de sequência. |
| linha cronológica | Uma string contendo a linha do tempo desejada para o posicionamento e o conteúdo do anúncio, que substitui e quebra no fluxo de conteúdo. | Não | Linha do tempo VOD (consulte o formato [de linha do tempo](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)VOD) |
| token | Ativar tokens de autorização de segmento TS Observação:  Somente tokens CDN do Akamai são suportados | Para tokens de autorização de segmento TS | Booleano |
| modo de rastreamento | Ativar o rastreamento de anúncios; personalizado do lado do cliente (simples), do lado do servidor (sstm) ou híbrido (simplesstm). | Não | simples, sstm ou simplesstm Observação:  Se esse parâmetro não estiver incluído, #EX-X-MARKER será inserido no manifesto. Ver Diretiva [](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md)EXT-X-MARKER. |
| posição | Instrui o servidor manifest a retornar somente informações de rastreamento de anúncios. Não especifique esse parâmetro na solicitação de bootstrap. | Rastreamento do cliente | Nota alfanumérica:  O servidor manifest ignora todos os valores transmitidos. No entanto, se você passar uma string nula ou vazia, o servidor manifest retornará o M3U8 em vez de informações de rastreamento. |
| pttrackingversion | A versão de formato das informações de rastreamento do lado do cliente. | Rastreamento do cliente | v1 , v2 , v3 ou vmap |
| scteTracking | Procure M3U8 , antes que as informações de rastreamento SCTE possam ser obtidas no sidecar JSON V2.  <br/>Este parâmetro indica ao servidor manifest que o player que está buscando o M3U8 precisa que as informações da tag SCTE sejam recuperadas. | Não (padrão:  false ) | true ou false Observação:  Os dados SCTE-35 são retornados no auxiliar JSON com a seguinte combinação de valores de parâmetro de consulta: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35` </li><li>pttrackingversion=v2 </li><li>scteTracking=true</li></ul> |
| vetargetmultiplicador | O número de segmentos a partir do ponto ativo O deslocamento de precedente é configurado usando:   `(  vetargetmultiplier  *  targetduration ) +  vebufferlength` Observação <br/><br/>****:  Somente ao vivo/linear | Não (padrão:  3.0 ) | Flutuar |
| vebufferLength | O número de segundos a partir do ponto ativo Nota:  Somente ao vivo/linear | Não (padrão:  3.0 ) | Flutuar |
