---
title: Parâmetros de consulta do servidor de manifesto
description: Os parâmetros de consulta informam ao servidor de manifesto que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor de manifesto faça. Alguns são obrigatórios e outros têm formatos ou valores aceitáveis específicos.
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---


# Parâmetros de consulta do servidor de manifesto {#ms-query-params}

Os parâmetros de consulta informam ao servidor de manifesto que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor de manifesto faça. Alguns são obrigatórios e outros têm formatos ou valores aceitáveis específicos.

O URL completo consiste no URL base seguido por um ponto de interrogação e, em seguida, `parameterName=value` argumentos, separados por &quot;E&quot; comercial: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Parâmetros reconhecidos {#section_072845B7FA94468C8068E9092983C9E6}

O servidor de manifesto reconhece os parâmetros a seguir. Ele os processa ou transmite, juntamente com todos os parâmetros não reconhecidos, para o servidor de anúncios.

| Chave | Descrição | Obrigatório | Valores válidos |
|---|---|---|---|
| `__sid__` | ID exclusiva que o servidor de manifesto usa para gerar a ID da sessão. | Sim | Alfanumérico |
| g | Tipo de dispositivo cliente | Quando as regras de direcionamento dependem do tipo de dispositivo | Consulte a lista em [Tipos de cliente](https://adobeprimetime.zendesk.com). Requer acesso ao Zendesk. |
| k | Palavras-chave para direcionamento de anúncios personalizados | Não | String segura para URL no formato `key1=value1;key2=value2;. . .` |
| u | ID do ativo de inserção de anúncio do Primetime. | Sim | Valor de hash MD5 |
| z | ID da zona de inserção de anúncio do Primetime do ativo. | Sim | Integer |
| enableC3 | O cliente está em uma janela C3. Se verdadeiro, substituir apenas dispons locais; caso contrário, substituir todas dispons. | Não | Booleano |
| live | Indica se o conteúdo é um fluxo Live ou VOD (video on-demand). | Akamai Ad Scaler ou cliente do iOS Safari. | Booleano |
| `pabimode` | [Habilitar inserção parcial de ad break](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) suporte. <br> Ative se for verdadeiro ou inicie.<br> Desativar se falso. | Não (o padrão está desabilitado) | start, true ou false |
| `ptadwindow` | Duração (segundos) da janela de compilação do anúncio: até que ponto procurar anúncios quando um usuário de DVR ingressa no fluxo. | Não (padrão = 1800) | 0 a 1800 |
| `ptassetid` | Identificador exclusivo do conteúdo atribuído e mantido pelo publicador. | Akamai Ad Scaler | Sequência de caracteres segura para URL |
| `ptcdn` | Lista de um ou mais CDNs para hospedar ativos transcodificados. Consulte [Suporte a vários CDNs](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | Não (padrão=Akamai) | Exemplo: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | O nome do formato de sinalização de anúncio personalizado presente no M3U8. | Não | DPISimple, DPIScte35, Elemental, NBC, NFL ou Turner |
| `ptfailover` | Sinaliza ao servidor de manifesto para identificar fluxos primários e de failover especificados na lista de reprodução principal e para tratá-los como conjuntos separados. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS). Consulte  [Facilitando a alternância do reprodutor HLS](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | Não | true |
| `ptmulticall` | Se definido como verdadeiro, várias chamadas de anúncio do Auditude para o FER serão feitas; uma para cada ad-break. Se ausente ou definido como falso, uma chamada de anúncio é feita para auditar o FER. | Não | Booleano <br> **Nota**: os seguintes requisitos: <ul><li>`ptcueformat` o parâmetro deve ser definido como nbc</li><li>O parâmetro pttimeline é ignorado.</li></ul> |
| `ptplayer` | Jogador fazendo a solicitação. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Gerado automaticamente pela inserção de anúncios e usado pelo Akamai. Não adicione nem remova. | Akamai Ad Scaler |  |
| `pttagds` | Ativar [EXT-X- SEQUÊNCIA DE DESCONTINUIDADE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3) tags | Não | true - o servidor de manifesto inclui uma tag de sequência antes do conteúdo em cada arquivo m3u8 enviado; se o parâmetro não estiver presente ou não for true, o servidor de manifesto não incluirá uma tag de sequência. |
| `pttimeline` | Uma string que contém a linha do tempo desejada para a inserção e o conteúdo do anúncio, que substitui os ad breaks no fluxo de conteúdo. | Não | [Linha do tempo de VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Habilite os tokens de autorização do segmento TS.<br> **Nota**: somente tokens CDN do Akamai são compatíveis | Para tokens de autorização do segmento TS | Booleano |
| `pttrackingmode` | Ative o rastreamento de anúncios; personalizado do lado do cliente (simples), do lado do servidor (sstm) ou híbrido (simplesstm). | Não | simple, sstm ou simplesstm.<br> **Nota**: Se esse parâmetro não for incluído, #EX-X-MARKER será inserido no manifesto. Consulte [Diretiva EXT-X-MARKER](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Instrui o servidor de manifesto a retornar somente informações de rastreamento de anúncios. Não especifique este parâmetro na solicitação de inicialização. | Rastreamento do lado do cliente | Observação alfanumérica: o servidor de manifesto ignora todos os valores transmitidos. No entanto, se você passar uma cadeia de caracteres nula ou vazia, o servidor de manifesto retornará o M3U8 em vez de informações de rastreamento. |
| `pttrackingversion` | A versão de formato das informações de rastreamento do lado do cliente. | Rastreamento do lado do cliente | v1, v2, v3 ou vmap |
| `scteTracking` | Busque M3U8 , antes que as informações de rastreamento do SCTE possam ser buscadas no sidecar do JSON V2. <br>Esse parâmetro indica ao servidor de manifesto que o reprodutor que busca o M3U8 precisa que as informações da tag SCTE sejam recuperadas. | Não (padrão: falso) | verdadeiro ou falso. <br> **Nota**: os dados SCTE-35 são retornados no JSON sidecar com a seguinte combinação de valores de parâmetro de consulta: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | O número de segmentos do ponto ativo O deslocamento antes da exibição é configurado usando: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Nota**: somente Live/Linear | Não (padrão: 3.0) | Flutuante |
| `vebufferLength` | O número de segundos a partir do ponto ativo. **Nota**: somente Live/Linear. | Não (padrão: 3.0) | Flutuante |
