---
title: API do Bootstrap
description: API do Bootstrap
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# API do Bootstrap {#bootstrap-api}

Normalmente, a API do Bootstrap é o URL enviado para as APIs de reprodução de vídeo/cliente.  Para opções e parâmetros que podem ser configurados, consulte o [Parâmetros da API do Bootstrap](#bootstrap-api-parameters).

## Enviar um comando para o Servidor de manifesto {#send-a-command-to-the-manifest-server}

1. Enviar um `HTTP GET` solicitação de um URL de inicialização construído usando o seguinte padrão:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **Extensão de arquivo** Definido. `.m3u8` se o manifesto do público alvo for HLS, `.mpd` se os manifestos do público alvo estiverem no DASH.

   * **PublisherAssetID** Obrigatório. Identificador exclusivo do editor para o conteúdo específico.

   * **URL de conteúdo** Obrigatório. URL do arquivo de conteúdo M3U8, Base64 codificado para ser seguro no URL do servidor de manifesto. O URL de conteúdo deve apontar para um arquivo M3U8 variante, mesmo se houver apenas um fluxo de taxa de bits.

   * **Parâmetros de consulta** Estes constituem a parte mais variada do pedido. Eles informam ao servidor de manifesto que tipo de cliente está fazendo a solicitação e o que ele deseja que o servidor de manifesto faça.

   Por exemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitações HTTP vs. HTTPS**

   O servidor de manifesto cria URLs usando o mesmo protocolo HTTP da solicitação do cliente. Se um reprodutor fizer uma solicitação HTTP (http) não segura, o servidor de manifesto retornará URLs de manifesto e URLs de rastreamento de Auditude com o protocolo http. Se um player fizer uma conexão HTTP segura (https), o servidor de manifesto, ele retornará URLs de manifesto e URLs de rastreamento de Auditude com o protocolo https.

   >[!NOTE]
   >
   >O servidor de manifesto não pode alterar o protocolo (HTTP ou HTTPS) de beacons de rastreamento de terceiros. Você deve entrar em contato com o conteúdo e provedores de anúncios de terceiros para que eles configurem os protocolos desejados.  Os protocolos de URL de segmentos podem ser alterados. No entanto, por padrão, use os mesmos protocolos definidos nos manifestos de destino.

## Parâmetros da API do Bootstrap {#bootstrap-api-parameters}

Os parâmetros de consulta informam ao servidor de manifesto que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor de manifesto faça. Alguns são obrigatórios e outros têm formatos ou valores aceitáveis específicos.
O URL completo consiste no URL base seguido por um ponto de interrogação e, em seguida, `parameterName=value` argumentos separados por &quot;E&quot; comercial. Por exemplo, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

O servidor de manifesto reconhece os parâmetros a seguir. Toda a sequência de consulta\
Os parâmetros do são passados para o servidor de publicidade.

| parâmetro | descrição | formatos |
|---|---|---|
| _sid_ | Uma ID exclusiva que o servidor de manifesto usará para gerar a ID da sessão. | Obrigatório para DASH/HLS |
| live | Notifica ao Ad Insertion do Primetime que o item de conteúdo transmitido é um fluxo ao vivo.  Se esse parâmetro não for transmitido, a inserção de anúncio do Primetime fará uma solicitação secundária na chamada de manifesto inicial para determinar se o manifesto está ativo ou vod.<br>Valores possíveis:<br>verdadeiro para conteúdo ao vivo<br>falso para conteúdo de vod<br>omitir para detecção automática | Opcional para HLS.  Obrigatório para DASH |
| z | A ID da zona do ativo que precisa ser fornecido para o Ad Insertion do Primetime. Fornecido pelo Gerente técnico de conta do Adobe. | Obrigatório para DASH/HLS |
| pabimode | Habilita [inserção parcial de ad break](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) para transmissões ao vivo.<br>Valores possíveis:<br>true para habilitar<br>omitir para desativar (desativado por padrão) | HLS/DASH |
| ptadtimeout | Permite a limitação do tempo geral de resolução do anúncio, se os provedores downstream demorarem muito para responder.  Respostas de longa duração podem causar problemas com a reprodução. Isso permite que o DAI do Primetime force uma resposta em um limite de tempo específico.<br>Valores possíveis:<br>sequência numérica em milissegundos.<br>omitir para desativar (desativado por padrão) | HLS/DASH |
| ptadwindow | Duração (em segundos) da janela de lookback ad decisioning — até que ponto o Primetime Ad Insertion procurará dicas de anúncios quando um usuário do DVR entrar no fluxo. Um valor zero desativará a decisão de anúncios intermediários no manifesto inicial, com a decisão sendo retomada somente após a primeira atualização. Esse parâmetro é útil para desativar a inserção de anúncios em sessões que podem durar apenas alguns segundos (também conhecido como inversão de canal).<br>Valores possíveis:<br>sequência numérica 0-1800 (padrão 1800) | Somente HLS |
| ptassetid | Identificador exclusivo do conteúdo atribuído e mantido pelo publicador.  Obrigatório quando usado em conjunto com o Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Lista de um ou mais CDNs para hospedar ativos transcodificados. Para obter mais informações, consulte [Entrega e armazenamento](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Valores possíveis:<br>akamai, level3, llnw (redes de luz), comcast.<br>Por padrão, são usados CDNs de Ad Insertion do Primetime. | HLS/DASH |
| ptcueformat | O formato especificado de tags para executar a decisão de anúncios (por exemplo, scte35).<br>Valores possíveis:<br>dpisimple, dpiscte35, elemental<br>Para formatos de sinalização personalizados, entre em contato com o representante técnico da conta para obter o valor a ser usado no caso de uso | HLS/DASH |
| ptfailover | Sinaliza ao servidor de manifesto para identificar fluxos primários e de failover especificados na lista de reprodução principal e para tratá-los como conjuntos separados. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS.) Para obter mais informações, consulte [Facilitando a alternância do reprodutor HLS](hls-switching-to-failover.md) | Somente HLS |
| ptmulticall | Se ativado, uma solicitação de anúncio separada é feita para cada uma das vantagens encontradas em um ativo de VOD.  Por padrão, o Primetime Ad Insertion tentará coletar todas as informações disponíveis e enviá-las para o servidor de publicidade em uma solicitação. Valores possíveis:true para habilitar, <br>omitir para desativar (desativado por padrão) | HLS/DASH |
| ptparallelstream | Permite que clientes com players que solicitam fluxos de áudio ou vídeo desmesclados do CMAF em paralelo para garantir que os anúncios em trilhas de áudio e vídeo sejam consistentes. | Somente HLS |
| ptprotoswitch | Habilita regras nomeadas de regravação de manifesto e de busca de anúncios, que normalmente serão configuradas pelo representante do suporte técnico.<br>Exemplo: adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | Habilita a injeção de tags EXT-X-DISCONTINUITY-SEQUENCE em cabeçalhos HLS. Valores possíveis: true para habilitar a omissão para desabilitar (desabilitado por padrão) | Somente HLS |
| pttimeline | Uma string que contém a linha do tempo desejada para a inserção e o conteúdo do anúncio, que substitui os ad breaks no fluxo de conteúdo. [Consulte Formato da linha do tempo de VOD] | HLS/DASH |
| pttoken | Habilita esquemas de proteção de token de autorização de fragmento/segmento de conteúdo para CDNs<br>Valores possíveis:<br>akamai, llnw (limelight), ctl (centurylink) (a geração de tokens padrão está desativada) | HLS/DASH |
| pttrackingmode | Habilite os esquemas de rastreamento de anúncios.<br>Valores possíveis:<br>simples para rastreamento de anúncios no lado do cliente<br>sstm para rastreamento de anúncios do lado do servidor<br>simple stm para rastreamento de anúncio de cliente/servidor híbrido (por padrão, nenhum rastreamento de anúncio é executado) | HLS/DASH |
| pttrackingposition | Instrui o servidor de manifesto a retornar somente informações de rastreamento de anúncios. Não especifique este parâmetro na solicitação de inicialização.<br>Observação: o servidor de manifesto ignora todos os valores transmitidos. No entanto, se você passar uma string nula ou vazia, o servidor de manifesto retornará o M3U8 | HLS/DASH<br>Rastreamento do lado do cliente |
| pttrackingversion | Define a versão de formato a ser retornada.<br>Valores possíveis:<br>v1, v2, v3 ou vmap | HLS/DASH<br>Rastreamento do lado do cliente |
| scteTracking | Esse parâmetro indica ao servidor de manifesto que o reprodutor que busca o M3U8 precisa que as informações da tag SCTE sejam recuperadas.<br>Valores possíveis:<br>verdadeiro ou falso (padrão falso)<br>Observação: os dados SCTE-35 são retornados no JSON sidecar com a seguinte combinação de valores de parâmetro de consulta:<br>ptcueformat=turner | elemental | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | Somente HLS |
| vetargetmultiplier | O número de segmentos do ponto ativo O deslocamento antes da exibição é configurado usando: ( vetargetmultiplier * targetduration ) + vebufferlength<br>Observação: esse parâmetro se aplica somente a fluxos Live/Linear HLS<br>Valores possíveis:<br>flutuante numérico<br>(padrão: 3.0 - igual à especificação HLS) | Somente HLS |
| vebufferLength | O número de segundos a partir do ponto ativo, usado em conjunto com vetargetmultiplier.<br>Observação: esse parâmetro se aplica somente a fluxos Live/Linear HLS<br>Valores possíveis:<br>flutuante numérico<br>(padrão: 3.0) | Somente HLS |
