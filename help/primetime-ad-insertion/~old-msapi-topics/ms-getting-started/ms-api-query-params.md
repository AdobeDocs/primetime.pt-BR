---
title: Parâmetros do query do servidor manifest
description: Os parâmetros do query informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.
seo-title: Parâmetros do query do servidor manifest
seo-description: Os parâmetros do query informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---


# Parâmetros de query do servidor manifest {#ms-query-params}

Os parâmetros do query informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.

O URL completo consiste no URL básico seguido por um ponto de interrogação e, em seguida, `parameterName=value` argumentos, separados por E comercial: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parâmetros reconhecidos {#section_072845B7FA94468C8068E9092983C9E6}

O servidor manifest reconhece os seguintes parâmetros. Processa-os ou os transmite, juntamente com todos os parâmetros não reconhecidos, para o servidor de anúncios.

| Principal | Descrição | Obrigatório | Valores Válidos |
|---|---|---|---|
| `__sid__` | ID exclusiva que o servidor manifest usa para gerar a ID da sessão. | Sim | Alfanumérico |
| g | Tipo de dispositivo cliente | Quando as regras de definição de metas dependem do tipo de dispositivo | Consulte lista em [Tipos de cliente](https://adobeprimetime.zendesk.com). Requer acesso ao Zendesk. |
| k | Palavras-chave para direcionamento de anúncio personalizado | Não | Sequência segura para URL no formato `key1=value1;key2=value2;. . .` |
| u | ID do ativo de inserção do anúncio Primetime. | Sim | Valor de hash MD5 |
| z | Primetime e ID de Zona de inserção do ativo. | Sim | Número inteiro |
| enableC3 | O cliente está em uma janela C3. Se verdadeiro, substitua apenas os valores locais; caso contrário, substitua todos os disponíveis. | Não | Booleano |
| live | Indica se o conteúdo é um fluxo ao vivo ou VOD (vídeo sob demanda). | Akamai Ad Scaler ou cliente iOS Safari. | Booleano |
| `pabimode` | [Habilite Suporte para inserção parcial e ](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) quebra. <br> Ative se verdadeiro ou start.<br> Desative se falso. | Não (o padrão está desativado) | start, verdadeiro ou falso |
| `ptadwindow` | Duração (segundos) da janela de identificação do anúncio: até que ponto procurar anúncios quando um usuário de DVR ingressar no stream. | Não (padrão = 1800) | 0 a 1800 |
| `ptassetid` | ID exclusiva do conteúdo atribuído e mantido pelo editor. | Akamai Ad Scaler | Sequência segura para URL |
| `ptcdn` | Lista de um ou mais CDNs para hospedar ativos transcodificados. Consulte [Suporte a vários CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | Não (padrão=Akamai) | Exemplo: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | O nome do formato de sinalização de anúncio personalizado presente no M3U8. | Não | DPISimple, DPIScte35, Elemental, NBC, NFL ou Turner |
| `ptfailover` | Sinaliza o servidor manifest para identificar fluxos primários e de failover especificados na lista de reprodução principal e para tratá-los como conjuntos de disjunção. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS). Consulte [Facilitando a alternância do player HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | Não | true |
| `ptmulticall` | Se definido como true, várias chamadas publicitárias do Auditude para FER serão feitas; uma para cada pausa de anúncio. Se ausente ou definido como false, uma chamada ad-call é feita para auditude para FER. | Não | Booleano <br> **Observação**: Os seguintes requisitos: <ul><li>`ptcueformat` parâmetro deve ser definido como nbc</li><li>o parâmetro da linha do tempo é ignorado.</li></ul> |
| `ptplayer` | Jogador que faz a solicitação. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Gerado automaticamente por inserção de anúncio e usado pelo Akamai. Não adicione nem remova. | Akamai Ad Scaler |  |
| `pttagds` | Habilitar tags [EXT-X- DISCONTINUITY- SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | Não | true - o servidor manifest inclui uma tag de sequência antes do conteúdo de cada arquivo m3u8 que enviar; se o parâmetro não estiver presente ou não for verdadeiro, o servidor manifest não incluirá uma tag de sequência. |
| `pttimeline` | Uma string contendo a linha do tempo desejada para o posicionamento e o conteúdo do anúncio, que substitui e quebra no fluxo de conteúdo. | Não | [Linha do tempo VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Ativar tokens de autorização de segmento TS.<br> **Observação**: Somente tokens CDN do Akamai são suportados | Para tokens de autorização de segmento TS | Booleano |
| `pttrackingmode` | Ativar o rastreamento de anúncios; personalizado do lado do cliente (simples), do lado do servidor (sstm) ou híbrido (simplesstm). | Não | simples, sstm ou simplesstm.<br> **Observação**: Se esse parâmetro não estiver incluído, #EX-X-MARKER será inserido no manifesto. Consulte [Diretiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Instrui o servidor manifest a retornar somente informações de rastreamento de anúncios. Não especifique esse parâmetro na solicitação de bootstrap. | Rastreamento do cliente | Nota alfanumérica:  O servidor manifest ignora todos os valores transmitidos. No entanto, se você passar uma string nula ou vazia, o servidor manifest retornará o M3U8 em vez de informações de rastreamento. |
| `pttrackingversion` | A versão de formato das informações de rastreamento do cliente. | Rastreamento do cliente | v1, v2, v3 ou vmap |
| `scteTracking` | Procure M3U8 , antes que as informações de rastreamento SCTE possam ser obtidas no sidecar JSON V2. <br>Este parâmetro indica ao servidor manifest que o player que está buscando o M3U8 precisa que as informações da tag SCTE sejam recuperadas. | Não (padrão: falso) | verdadeiro ou falso. <br> **Observação**: Os dados SCTE-35 são retornados no auxiliar JSON com a seguinte combinação de valores de parâmetro de query: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | O número de segmentos a partir do ponto ativo O deslocamento de precedente é configurado usando: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**:  Somente ao vivo/linear | Não (padrão:  3,0) | Flutuar |
| `vebufferLength` | O número de segundos a partir do ponto ativo. **Observação**: Somente ao vivo/linear. | Não (padrão: 3,0) | Flutuar |
