---
title: API do Bootstrap
description: 'API do Bootstrap '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# API de Bootstrap {#bootstrap-api}

Normalmente, a API do Bootstrap é o URL enviado para as APIs de reprodução do cliente/vídeo.  Para opções e parâmetros que podem ser configurados, consulte os [parâmetros da API de Bootstrap](#bootstrap-api-parameters).

## Enviar um comando para o Servidor Manifesto {#send-a-command-to-the-manifest-server}

1. Envie uma solicitação `HTTP GET` para um URL de inicialização construído usando o seguinte padrão:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **Extensão** do arquivoDefined. `.m3u8` se o manifesto do público alvo for HLS,  `.mpd` se os manifestos do público alvo estiverem no DASH.

   * **** PublisherAssetIDRequired. ID exclusiva do editor para o conteúdo específico.

   * **Conteúdo** URLRequired. URL do arquivo M3U8 de conteúdo, Base64 codificado para ser seguro dentro do URL do servidor manifest. O URL do conteúdo deve apontar para um arquivo M3U8 variante, mesmo se houver apenas um fluxo de taxa de bits.

   * **Parâmetros de query** Estes são a parte mais variada da solicitação. Eles informam ao servidor manifest qual tipo de cliente está fazendo a solicitação e o que ele deseja que o servidor manifest faça.

   Por exemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitações HTTP vs. HTTPS**

   O servidor manifest cria URLs usando o mesmo protocolo HTTP da solicitação do cliente. Se um player fizer uma solicitação HTTP não segura (http), o servidor manifest retornará URLs de manifesto e URLs de rastreamento Auditude com o protocolo http. Se um player fizer uma conexão segura HTTP (https), servidor manifest, ele retornará URLs de manifesto e URLs de rastreamento Auditude com o protocolo https.

   >[!NOTE]
   >
   >O servidor manifest não pode alterar o protocolo (HTTP ou HTTPS) dos beacons de rastreamento de terceiros. Você deve entrar em contato com o conteúdo e os provedores de anúncios de terceiros para que eles configurem os protocolos desejados.  Os protocolos de URL de segmentos podem ser alterados, no entanto, por padrão, usar os mesmos protocolos definidos nos manifestos do público alvo.

## Parâmetros da API do Bootstrap {#bootstrap-api-parameters}

Os parâmetros do query informam ao servidor manifest que tipo de cliente enviou a solicitação e o que esse cliente deseja que o servidor manifest faça. Alguns são obrigatórios e alguns têm formatos ou valores aceitáveis específicos.
O URL completo consiste no URL básico seguido por um ponto de interrogação e, em seguida, `parameterName=value` argumentos separados por E comercial. Por exemplo, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

O servidor manifest reconhece os seguintes parâmetros. Todas as querystring\
são passados para o servidor de publicidade.

| parâmetro | descrição | formatos |
|---|---|---|
| _sid_ | Uma ID exclusiva que o servidor manifest usará para gerar a ID da sessão. | Obrigatório para DASH/HLS |
| live | Notifica o Primetime Ad Insertion que o item de conteúdo passado é um fluxo ao vivo.  Se esse parâmetro não for transmitido, a inserção do Anúncio Primetime fará uma solicitação secundária na chamada manifest inicial para determinar se o manifesto é live ou vod.<br>Valores possíveis:<br>true para live <br>contentfalse para vod <br>contentomit para detecção automática | Opcional para HLS.  Obrigatório para DASH |
| z | A ID de zona do ativo que precisa ser fornecido ao Primetime Ad Insertion. Fornecido pelo Gerente técnico de contas do Adobe. | Obrigatório para DASH/HLS |
| pabimode | Habilita [inserção parcial de anúncios](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) para fluxos ao vivo.<br>Valores possíveis:<br>true para <br>ativar omit para desativar (padrão desativado) | HLS/DASH |
| ptadtimeout | Permite limitar o tempo geral de resolução do anúncio, se os provedores downstream levarem muito tempo para responder.  Respostas de longa duração podem causar problemas na reprodução, o que permite que o Primetime DAI force uma resposta dentro de um limite de tempo específico.<br>Valores possíveis:sequência <br>numérica em milissegundos.<br>omit to disable (padrão desativado) | HLS/DASH |
| plataforma | Duração (em segundos) da janela de pesquisa e decisão do anúncio — até que ponto o Primetime Ad Insertion procurará dicas do anúncio quando um usuário do DVR ingressar no fluxo. Um valor de zero desativará a decisão de anúncio intermediário no manifesto inicial, com a decisão sendo retomada somente após a primeira atualização. Esse parâmetro é útil para desativar a inserção de anúncios em sessões que podem durar apenas alguns segundos (também conhecido como mudança de canal).<br>Valores possíveis:string <br>numérica 0-1800 (padrão 1800) | Somente HLS |
| ptassetid | ID exclusiva do conteúdo atribuído e mantido pelo editor.  Obrigatório quando usado em conjunto com o Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Lista de um ou mais CDNs para hospedar ativos transcodificados. Para obter mais informações, consulte [Delivery e armazenamento](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Valores possíveis:<br>akamai, level3, lnw (redes de luz de luz de fundo), comcast.<br>Por padrão, os Ad Insertion do Primetime são usados. | HLS/DASH |
| ptcueformat | O formato especificado de tags para executar a decisão de anúncio (por exemplo, scte35).<br>Valores possíveis:<br>detalhado, dpiscte35, <br>elementalPara formatos de sinalização personalizados, entre em contato com seu representante de conta técnica para obter o valor a ser usado no caso de uso | HLS/DASH |
| failover de canal | Sinaliza o servidor manifest para identificar fluxos primários e de failover especificados na lista de reprodução principal e para tratá-los como conjuntos de disjunção. Isso facilita o failover e evita erros de tempo. (Somente para dispositivos Apple HLS.) Para obter mais informações, consulte [Facilitando a alternância do player HLS](hls-switching-to-failover.md) | Somente HLS |
| tímulo | Se ativada, uma solicitação de anúncio separada é feita para cada valor encontrado em um ativo VOD.  Por padrão, o Primetime Ad Insertion tentará coletar todas as informações disponíveis e enviá-las para o servidor de publicidade em uma solicitação. Valores possíveis:true para ativar, <br>omit para desativar (padrão desativado) | HLS/DASH |
| ptparallelstream | Permite que os clientes com players que solicitam streams de áudio ou vídeo descompilados CMAF em paralelo, a fim de garantir que os anúncios nas faixas de áudio e vídeo sejam consistentes. | Somente HLS |
| protótipo | Habilita regras de regravação de manifesto nomeado e regras de busca de anúncios, que normalmente serão configuradas pelo representante de suporte técnico.<br>Exemplo: adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | Permite a injeção de tags EXT-X-DISCONTINUITY-SEQUENCE em cabeçalhos HLS.Valores possíveis:true para ativar omit para desativar (padrão desativado) | Somente HLS |
| linha cronológica | Uma string contendo a linha do tempo desejada para o posicionamento e o conteúdo do anúncio, que substitui e quebra no fluxo de conteúdo. [ Consulte Formato de linha do tempo VOD  ] | HLS/DASH |
| token | Habilita esquemas de proteção de token de fragmento/autorização de segmento de conteúdo para CDNs<br>Valores possíveis:<br>akamai, lnw (iluminação), ctl (ligação central) (a tokenização padrão está desativada) | HLS/DASH |
| modo de rastreamento | Habilite esquemas de rastreamento de anúncios.<br>Valores possíveis:<br>simples para <br>rastreamento de anúncio do cliente para <br>stm pararastreamento de anúncio do lado do servidor para rastreamento de anúncio híbrido do cliente/servidor (por padrão, nenhum rastreamento de anúncio é realizado) | HLS/DASH |
| posição | Instrui o servidor manifest a retornar somente informações de rastreamento de anúncios. Não especifique esse parâmetro na solicitação de bootstrap.<br>Observação: O servidor manifest ignora todos os valores transmitidos. Entretanto, se você passar uma string nula ou vazia, o servidor manifest retornará o M3U8 | Rastreamento HLS/DASH<br>do lado do cliente |
| pttrackingversion | Define a versão do formato a ser retornada.<br>Valores possíveis:<br>v1, v2, v3 ou vmap | Rastreamento HLS/DASH<br>do lado do cliente |
| scteTracking | Este parâmetro indica ao servidor manifest que o player que está buscando o M3U8 precisa que as informações da tag SCTE sejam recuperadas.<br>Valores possíveis:<br>true ou false (padrão false)<br>Observação: Os dados SCTE-35 são retornados no auxiliar JSON com a seguinte combinação de valores de parâmetro de query:<br>ptcueformat=turner | elementar | nfl | DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | Somente HLS |
| vetargetmultiplicador | O número de segmentos a partir do ponto ativo O deslocamento de precedente é configurado usando: ( vetargetmultiplier * targetduration ) + vebufferlength<br>Nota: Este parâmetro se aplica a fluxos HLS ao vivo/linear somente<br>Valores possíveis:<br>flutuante numérico<br>(padrão: 3.0 - igual à especificação HLS) | Somente HLS |
| vebufferLength | O número de segundos a partir do ponto ativo, usado em conjunto com o multiplicador vetorial.<br>Observação: Esse parâmetro se aplica a fluxos HLS ao vivo/linear <br>onlyValores possíveis:flutuação <br>numérica<br> (padrão: 3,0) | Somente HLS |
