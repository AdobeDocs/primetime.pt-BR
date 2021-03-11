---
title: Parâmetros de consulta do servidor de manifesto
description: Os parâmetros de consulta informam o servidor de manifesto que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor de manifesto faça. Alguns são obrigatórios e outros têm formatos ou valores aceitáveis específicos.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Parâmetros de consulta do servidor de manifesto {#ms-query-params}

Os parâmetros de consulta informam o servidor de manifesto que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor de manifesto faça. Alguns são obrigatórios e outros têm formatos ou valores aceitáveis específicos.

O URL completo consiste no URL base seguido por um ponto de interrogação e, em seguida, `parameterName=value` argumentos, separados por &quot;E&quot; comercial (&amp;): `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parâmetros reconhecidos {#section_072845B7FA94468C8068E9092983C9E6}

O servidor de manifesto reconhece os seguintes parâmetros. Ela os processa ou os transmite, juntamente com todos os parâmetros não reconhecidos, para o servidor de anúncios.

| Chave | Descrição | Obrigatório | Valores válidos |
|---|---|---|---|
| `__sid__` | ID exclusiva que o servidor de manifesto usa para gerar a ID da sessão. | Sim | Alfanumérico |
| g | Tipo de dispositivo cliente | Quando as regras de direcionamento dependem do tipo de dispositivo | Consulte a lista em [Tipos de cliente](https://adobeprimetime.zendesk.com). Requer acesso ao Zendesk. |
| k | Palavras-chave para direcionamento de anúncio personalizado | Não | Sequência segura para URL no formato `key1=value1;key2=value2;. . .` |
| u | ID de ativo de inserção de anúncio do Primetime. | Sim | Valor de hash MD5 |
| z | ID de zona de inserção de anúncio do Primetime para o ativo. | Sim | Número inteiro |
| enableC3 | O cliente está em uma janela C3. Se true, substitua apenas local available; caso contrário, substitua todas as opções disponíveis. | Não | Booleano |
| live | Indica se o conteúdo é um fluxo Live ou VOD (vídeo sob demanda). | Akamai Ad Scaler ou cliente do iOS Safari. | Booleano |
| `pabimode` | [Habilite o suporte à ](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) inserção parcial do ad break. <br> Ative se true ou start.<br> Desative se falso. | Não (o padrão está desativado) | start, true ou false |
| `ptadwindow` | Duração (segundos) da janela de identificação do anúncio: até que ponto procurar anúncios quando um usuário de DVR ingressar no stream. | Não (padrão = 1800) | 0 a 1800 |
| `ptassetid` | ID exclusiva do conteúdo atribuído e mantido pelo editor. | Escalonador de anúncios do Akamai | Sequência de caracteres segura para URL |
| `ptcdn` | Lista de uma ou mais CDNs para hospedar ativos transcodificados. Consulte [Suporte a vários CDN](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | Não (padrão=Akamai) | Exemplo: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | O nome do formato de sinalização de anúncio personalizado presente no M3U8. | Não | DPISimple, DPIScte35, Elemental, NBC, Liga Nacional, ou Turner |
| `ptfailover` | Sinaliza o servidor de manifesto para identificar fluxos primários e de failover especificados na lista de reprodução principal e para tratá-los como conjuntos de disjunção. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS). Consulte [Facilitando a alternância do reprodutor HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | Não | true |
| `ptmulticall` | Se definido como verdadeiro, várias chamadas de anúncio do Auditude para FER serão feitas; um para cada ad break. Se ausente ou definido como falso, uma chamada de anúncio é feita para auditude para FER. | Não | Booleano <br> **Observação**: Os seguintes requisitos: <ul><li>`ptcueformat` deve ser definido como nbc</li><li>o parâmetro da linha do tempo é ignorado.</li></ul> |
| `ptplayer` | Jogador que faz a solicitação. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Gerado automaticamente por inserção de anúncio e usado pelo Akamai. Não adicione ou remova. | Escalonador de anúncios do Akamai |  |
| `pttagds` | Habilitar tags [EXT-X- DISCONTINUITY- SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) | Não | true - o servidor manifest inclui uma tag de sequência antes do conteúdo em cada arquivo m3u8 que ele envia; se o parâmetro não estiver presente ou não for verdadeiro, o servidor de manifesto não incluirá uma tag de sequência. |
| `pttimeline` | Uma string contendo a linha do tempo desejada para o posicionamento do anúncio e conteúdo, que substitui e quebra no fluxo de conteúdo. | Não | [Linha do tempo VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Habilitar tokens de autorização de segmento TS.<br> **Observação**: Somente tokens Akamai CDN compatíveis | Para tokens de autorização de segmento TS | Booleano |
| `pttrackingmode` | Ativar o rastreamento de anúncios; do lado do cliente personalizado (simples), do lado do servidor (sstm) ou híbrido (simplesstm). | Não | simples, sstm ou simplesstm.<br> **Observação**: Se esse parâmetro não for incluído, o #EX-X-MARKER será inserido no manifesto. Consulte [Diretiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Instrui o servidor de manifesto a retornar somente as informações de rastreamento de anúncios. Não especifique esse parâmetro na solicitação de bootstrap. | Rastreamento do lado do cliente | Nota alfanumérica:  O servidor manifest ignora todos os valores transmitidos. No entanto, se você passar uma string nula ou vazia, o servidor de manifesto retornará o M3U8 em vez de informações de rastreamento. |
| `pttrackingversion` | A versão de formato das informações de rastreamento do lado do cliente. | Rastreamento do lado do cliente | v1, v2, v3 ou vmap |
| `scteTracking` | Busque M3U8 antes de obter informações de rastreamento do SCTE no sidecar JSON V2. <br>Esse parâmetro indica ao servidor de manifesto que o reprodutor que está buscando o M3U8 precisa de informações de tag SCTE para serem recuperadas. | Não (padrão: false) | verdadeiro ou falso. <br> **Observação**: Os dados SCTE-35 são retornados no sidecar JSON com a seguinte combinação de valores de parâmetro de consulta: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | O número de segmentos do ponto ativo O deslocamento antes da exibição é configurado usando: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**:  Somente Live/Linear | Não (padrão:  3.0) | Flutuar |
| `vebufferLength` | O número de segundos a partir do ponto ativo. **Observação**: Somente Live/Linear. | Não (padrão: 3.0) | Flutuar |
