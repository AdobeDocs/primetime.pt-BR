---
title: Notas de versão do TVSDK 1.4 para Desktop HLS
description: As Notas de versão do TVSDK para Desktop HLS descrevem as novidades ou alterações, os problemas resolvidos e conhecidos no TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5196'
ht-degree: 0%

---


# TVSDK 1.4 para Notas de versão do Desktop HLS {#tvsdk-for-desktop-hls-release-notes}

As Notas de versão do TVSDK para Desktop HLS descrevem as novidades ou alterações, os problemas resolvidos e conhecidos no TVSDK DHLS.

## Novos recursos {#new-features}

**1.4.31**

* **Suporte a várias CDN para anúncios CRS**

   * Por padrão, todos os ativos transcodificados serão hospedados na CDN Adobe no Akamai. Com a versão mais recente, o Adobe Creative Repackaging Service (CRS) fornece a capacidade de fazer upload dos anúncios transcodificados em várias CDNs, conforme especificado pelo cliente.
   * Novas APIs são adicionadas ao TVSDK para permitir a especificação do url criativo do CRS final quando o URL padrão não é usado. Consulte a documentação para saber como usar essas novas APIs.

### Novos recursos nas versões anteriores {#new-features-previous}

**1.4.30**

* **Métricas de faturamento**

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

**1.4.24**

* **Conexão de rede persistente**

Importante: Você deve ter pelo menos o Adobe Flash Player versão 22 ou posterior instalado.
Conexões de rede persistentes criam e armazenam uma lista interna de conexões de rede que podem ser reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede. As conexões de rede persistentes devem aumentar a eficiência e diminuir a latência no código de rede.

Nesta versão, esse recurso não é compatível com o Apple Safari e o Mozilla Firefox em um Mac.

**1.4.19**

* Suporte à integridade de fluxo para anúncios VPAID.
* Ativada a opção de guia Mudo no reprodutor Flash FP 20.0.0.267 para Firefox 42 e posterior ao corrigir o problema de travamento.

**1.4.18**

* O Primetime Desktop HLS TVSDK agora é compatível com criações de SWF linear VPAID 2.0 para permitir uma rica experiência de anúncio interativa em fluxo.

**1.4.10**

* **Ad Fallback, Daisy chaining in ad selection logic (Zendesk #3103)** Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Ad fallback for VAST and VMAP ads](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Biblioteca do Video Heartbeats (VHL) atualizada para a versão 1.5**

   * Capacidade de enviar metadados com início de vídeo e/ou início de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - Os heartbeats têm menos em média e menor tamanho.

**1.4.7**

* **Suporte para individualização no local**

Suporte para instalações no local do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para ir para um terminal diferente.

**1.4.6**

* **Criptografia AES de amostra (requer o Flash Player versão 17.0.0.134)**

A criptografia AES baseada em exemplo agora é compatível.

**1.4.2.**

* **Atualização da Biblioteca do Video Heartbeats (VHL) para a versão 1.4.0.1**

   * Adicionada a capacidade de agrupar diferentes casos de uso de análises, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete . O ad break é inferido das chamadas de método trackAdStart e trackAdComplete .
   * A propriedade do indicador de reprodução não é mais necessária ao rastrear anúncios.

**1.4.0**

* **Sinalização de blecaute com** substituição de conteúdo alternativoComo parte da atualização do TVSDK 1.4, o TVSDK agora também oferece suporte para entrar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos de manifesto em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remover/substituir** anúncios C3Agora, nenhum trabalho de preparação adicional é necessário para inserir dinamicamente novos anúncios em ativos de VOD (video-on-demand) que estão saindo da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova funcionalidade poderosa também é útil nos casos em que o conteúdo ao vivo/linear é transmitido durante a transmissão e é imediatamente suspenso para uso como conteúdo sob demanda, sem tempo adequado para &quot;limpar&quot; o ativo.

## Problemas resolvidos {#resolved-issues}

>[!NOTE]
>
>Todos os clientes TVSDK que usam CRS são altamente incentivados a atualizar para pelo menos TVSDK 1.4.32 no iOS, Android e Desktop HLS. Essa atualização será uma substituição direta da implementação do aplicativo existente. Após a atualização, verifique as solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo, Charles) para verificar se a versão no caminho reflete a versão 3.1. Por exemplo,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versão 1.4.41**

* Zendesk #33777 - Localhost token SWF para compilação de distribuição DHLS expirada.

   Atualização do token localhost para demonstração PMP no DHLS.

### Solução de problemas nas versões anteriores {#resolved-issues-previous}

**Versão 1.4.38**  (891)

* Zendesk #30731 - O TVSDK não reproduz vários anúncios VPAID em um AdBreak.

   Correção da reprodução de vários anúncios VPAID em um AdBreak.

* Zendesk #29968 - Double Billboard.

   O reprodutor de vídeo pode repetir o último segmento de um período em que ocorre uma mudança de ABR. Devido a isso, às vezes, o último segmento de pré-lançamento repetido. Isso foi corrigido.

**Versão 1.4.35**  (879)

* Zendesk #26058 - Suporta eventos VPAID nativos

**Versão 1.4.33**  (873)

* Zendesk #21701 - Envia o URL criativo original para solicitação de CRS 1401 em vez do url normalizado.

   O problema em que URLs já recompactadas estão sendo solicitadas para transcodificação foi corrigido, de acordo com o exigido pelo back-end do CRS.
* Zendesk # 26197 - Compressão anamórfica não reproduzida na Resolução de exibição desejada.

   **Observação**: Esse problema requer o player do Flash 24.0.0.194 ou posterior.

   O problema em que entradas ausentes nas tabelas de proporção eram usadas para calcular a largura de saída foi corrigido.

* Zendesk # 26840 - Falha na detecção HDCP no IE11 + Windows7 após segunda tentativa.

   **Observação**: Esse problema requer o player do Flash 24.0.0.218 ou posterior.

   Esse problema foi resolvido modificando o processamento da fila de mensagens principal do AdobeCP para iterar por toda a fila, em vez de apenas bloquear na primeira mensagem.

* Zendesk #27460 - A nova conta Akamai não consegue lidar com uma solicitação de CDN do POST.

   A nova conta CDN não pode lidar com uma solicitação de CDN de POST. Esse problema foi resolvido atualizando o código para fazer com que a solicitação de anúncio cdn.auditude.com fosse GET em vez de POST.
* Zendesk nº 27619 - Falha do Flash no Windows 10

   **Observação**: Esse problema requer o player do Flash 24.0.0.218 ou posterior.

   Esse problema foi resolvido evitando uma falha como resultado de URLs longos.

* Zendesk #28218 - O evento de rastreamento não é disparado enquanto o plackback do ponto de retomada

   Esse problema é o mesmo do Zendesk nº 26592. O problema em que as operações de busca eram permitidas quando o reprodutor de mídia está no estado PREPARED para fluxos VOD foi corrigido.

**Versão 1.4.32**  (867)

* O evento de rastreamento do Zendesk nº 26592 não é disparado quando a reprodução começa no ponto de retomada

O código não atualizava o item de ad break precedente quando o ponto de retomada não era zero. Esse problema foi resolvido adicionando lógica para atualizar o código quando as horas de início do intervalo não correspondem.

* Zendesk #27022 Os anúncios não são reproduzidos na segunda vez em que um ativo é reproduzido

As exceções com os métodos de matriz foram corrigidas.

**Versão 1.4.30**  (855)

Os seguintes problemas foram resolvidos para TVSDK nesta versão:

* Zendesk #22898 - As legendas ausentes não devem causar falha na reprodução.

**Observação**: Esse problema requer o player do Flash 23.0.0.185 ou posterior.

Esse problema foi resolvido permitindo que o TVSDK continuasse a reprodução, mesmo que o manifesto estivesse faltando o WebVTT M3U8, e apenas registrasse um aviso.

* Zendesk #23454 - Anúncios de terceiros (VPAID) não são tratados corretamente

Esse problema foi resolvido lidando com anúncios VPAID corretamente com base em IDs de conteúdo em vez de intervalos de tempo.

* Zendesk #24528 - Métricas de uso de TVSDK para faturamento.

Importante: Esse problema requer o player do Flash 23.0.0.185 ou posterior.

* Problema de legenda oculta do Zendesk # 25432 durante o redimensionamento do reprodutor.

Importante: Esse problema requer o player do Flash 23.0.0.185 ou posterior.

O código do mapa de textura de exibição da legenda foi corrigido para manipular corretamente as coordenadas durante o redimensionamento do reprodutor.

A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

* Zendesk #23730 - As métricas de taxa de bits estão vazias

Esse problema foi resolvido rastreando as alterações da taxa de bits no VideoAnalyticsTracker.

* Adição de uma nova API, assetDuration, a PTVideoAnalyticsTrackingMetadata para atualizar a duração do ativo para fluxos Live/Lineares.

**Versão 1.4.28**  (848)

* Zendesk #25027 - Auditude não funciona na versão 1.4.27 do desktop

Esse problema foi resolvido adicionando o código para verificar o AUDITUDE_METADATA_KEY e tornando o AUDITUDE_METADATA_KEY e o ADVERTISING_METADATA_KEY intercambiáveis.

* Zendesk # 24428 - Problema de buffer frequente usando TVSDK para reproduzir um HLS de DRM

Esse problema foi resolvido considerando que, quando não há configuração de anúncio, o TVSDK pode acelerar o processamento, eliminando a retenção de anúncio precedente e a retenção de reserva ao vivo na linha do tempo projetadas para sincronizar a inserção de anúncio.

* Zendesk #24344 - Desative os arquivos WebVTT para melhorar o tempo de inicialização.

**Observação**: Esse problema requer o reprodutor do Flash 23 ou posterior.

Esse problema foi resolvido carregando os arquivos WebVTT somente quando as legendas precisam ser exibidas.

* Zendesk # 24994 - As legendas ocultas são descartadas do reprodutor ao retornar do intervalo comercial

**Observação**: Esse problema requer o reprodutor do Flash 23 ou posterior.

O código EOC espúrio fazia com que a exibição da legenda desaparecessem. Esse problema foi resolvido forçando os 608 códigos de legendas RU2, RU3 e RU4 a fornecer a visibilidade correta na janela ativa atual.

**Versão 1.4.27**  (844)

* Zendesk #21554 - Beacons de erro TVSDK não acionados para application-type = video/mp4

Esse problema foi resolvido habilitando o TVSDK a fazer o ping dos URLs de rastreamento de erros corretos nos formatos de ativos inválidos.

* Zendesk nº 23402 - Reprodução de anúncio incompleta

**Observação**: Esse problema requer o reprodutor do Flash 23 ou posterior.

Após receber um erro 404 em determinadas solicitações, pode ocorrer uma falha. Esse problema foi resolvido garantindo que a conexão não fosse encerrada enquanto a resposta estivesse sendo tratada. A resolução garante que os arquivos de anúncio VPAID não sejam contados incorretamente, de modo que não sejam liberados durante o download.

* Zendesk #23621 - Retry is failed on 400 and 404

**Observação**: Esse problema requer o reprodutor do Flash 23 ou posterior.

Correção do problema que causava a corrupção de metadados DRM ao alternar entre perfis diferentes.

* Zendesk #23705 - Vídeo de anúncio congelado durante pausas com título de anúncio

**Observação**: Esse problema requer o reprodutor do Flash 23 ou posterior.

Esse problema é o mesmo do Zendesk nº 23621.

* Zendesk #23905 - Algumas pausas de anúncio ignoradas nos ad breaks

**Observação**: Esse problema requer o reprodutor do Flash 23 ou posterior.

O código de rede nativo do Windows foi corrigido para garantir que as conexões não fechem alças que estão sendo usadas atualmente por outras conexões.

* Tíquete #24029 - Os fluxos de FER HLS não reproduzem todos os anúncios intermediários no arquivo .json intermediário.

Esse problema foi resolvido permitindo que os clientes definissem parâmetros personalizados separadamente na instância da Oportunidade, de modo que os clientes não precisassem substituir o OpportunityGenerator.

**Versão 1.4.26**  (839)

* Zendesk #18854 - Atualizar lógica de seleção criativa com base nas regras do CRS
   * Fornecido suporte para atualizar a lógica de seleção criativa com base nas regras do CRS

* Zendesk #22725 - playbackManager.beginPlayback() no aplicativo de amostra para Desktop

   * Correção da remoção dessa chamada redundante no final de startPlaybackFromFlashVars, pois o método é chamado de setupVideo()

* Zendesk #22807 - Exceção de referência nula do SeekManager

   * Corrigido fornecendo a proteção necessária de ponteiro NULL dentro do SeekManager relacionada ao _dispatcher

* Zendesk #22822 - Buffering frequente ao usar TVSDK para reproduzir um HLS claro

   * Corrigido pela remoção da oportunidade inicial gerada por adSignalingModeOpportunityGenerator se não houver anúncio

* Zendesk #23378 - A integridade do fluxo bloqueia rules.xml

   * Correção ao carregar o arquivo rules.xml por meio do fluxo de trabalho de integridade

**Versão 1.4.24**  (817)

* Zendesk #19851 - Quando o reprodutor se adapta a uma taxa de bits diferente, ele pula alguns quadros de volta no tempo na nova taxa de bits, tornando uma experiência estranha

**Observação**: Esse problema requer o player do Flash 22.0.0.175 ou posterior.

O problema em que o adaptador DRM é redefinido após o download de uma pequena fração de um segmento não é restaurado corretamente foi resolvido.

* Zendesk #20784 - Analytics: Acionamento de conclusões de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido com a adição de uma API (trackVideoComplete) para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo LINEAR/LIVE.

As seguintes bibliotecas foram atualizadas:

* Zendesk #21643 - Os anúncios VPAID não são reproduzidos na íntegra

   * Biblioteca AdobeMobile para 4.10.0
   * Biblioteca do VHL para 1.5.6
   * Biblioteca VHL-Nielsen para 1.6.7

Esse problema foi resolvido usando uma janela de visualização de altura zero para preencher o estágio em que um anúncio VPAID está sendo reproduzido.

* Zendesk #22110 - Analytics: Adicione um campo h:sc:ssl às chamadas de rastreamento de pulsação

Os problemas relacionados ao SSL foram corrigidos, e a biblioteca do VHL usada no TVSDK foi atualizada para a versão mais recente.

* Zendesk #22608 - Vídeo mostra intermitentemente uma tela preta (requer o Flash Player 22.0.0.175 ou posterior)

Durante a taxa de bits adaptável, com o limite de taxa de bits máxima, o recarregamento do vídeo mostra, intermitentemente, uma tela preta, mesmo que o cliente veja as atualizações na posição, e o cliente se comporta como se estivesse reproduzindo o conteúdo.

**Versão 1.4.23**  (809)

* Zendesk #2887 - Problema de ignoração de anúncio posterior quando a lógica de Regra de anúncio é aplicada ao TVSDK

**Observação**: Esse problema requer o player do Flash 21.0.0.240 ou posterior.

O problema em que os anúncios posteriores eram ignorados quando a lógica da regra de anúncio era aplicada ao TVSDK foi corrigido.

* Zendesk #19863 - Anúncio com arquivo de mídia VPAID descartado

Se um grande anúncio em linha tiver vários arquivos de mídia com um anúncio VPAID sendo o primeiro, o anúncio em linha não será reproduzido para fluxos ao vivo. Esse problema foi resolvido ao selecionar um arquivo de mídia diferente.

* Zendesk # 21021 - Áudio de ligação tardia que causa repetição de segmentos de áudio

**Observação**: Esse problema requer o player do Flash 21.0.0.240 ou posterior.

O problema de repetição de áudio foi corrigido.

* Zendesk #21125 - Retorno de pausa de anúncio ao vivo/linear antecipado

**Observação**: Esse problema requer o player do Flash 21.0.0.240 ou posterior.

Esta versão oferece suporte para retornar de um ad break antes da reprodução até a conclusão do ad break. O retorno antecipado é indicado por meio de uma tag de manifesto personalizada.

* Zendesk # 21369 O áudio de ligação tardia causa um tempo inconsistente

**Observação**: Esse problema requer o player do Flash 21.0.0.240 ou posterior.

O problema de repetição de áudio corrigido também corrigiu esse problema.

* Zendesk #21760, 20921 - Audio Video Desync on Seek (Sincronização de vídeo de áudio em busca).

**Observação**: Esse problema requer o player do Flash 21.0.0.240 ou posterior.

O problema de repetição de áudio foi corrigido.

* Zendesk #22024 - Erro ao executar o TVSDK

O problema no qual o reprodutor de referência não reproduzia nenhum fluxo e estava gerando uma exceção na inicialização foi corrigido.

**Versão 1.4.22**  (791)

* Zendesk #17580 - Erro de tempo de execução do Primetime com código 3357

**Observação**: Esse problema requer o player do Flash 21.0.0.197 ou posterior.

Os erros 3357 aleatórios que ocorreram ao inicializar corretamente o deviceID quando storeVoucher() é chamado foram corrigidos.

* Zendesk #21334 - Valor de tempo limite da solicitação de anúncio TVSDK para solicitações de anúncios de terceiros

Nesta versão, o tempo limite da solicitação de anúncio global foi adicionado.

**Versão 1.4.21**  (782)

* O Zendesk #19580 TVSDK aguarda a conclusão do resolvedor de conteúdo antes de enviar `PTTimedMetadataChangedNotification` notificações

**Observação**: Esse problema requer o player do Flash 21.0.0.182 ou posterior.

Esse problema foi resolvido no reprodutor de referência para desktop, fornecendo a capacidade de definir tags de anúncio e adicionar um gerador de oportunidade personalizado que mostra como assinar dicas personalizadas e como processar essas dicas em um arquivo VOD.

* O Zendesk #20806 Futuros anúncios intermediários na janela DVR não será acionado após a troca de câmeras

**Observação**: Esse problema requer o player do Flash 21.0.0.182 ou posterior.

Esse problema foi resolvido ao atualizar o aplicativo para definir _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) para desativar a inserção de anúncio precedente em uma troca de PIP e, como resultado, nenhuma oportunidade antes da exibição é gerada.

Uma funcionalidade de classificação foi introduzida para corrigir o posicionamento de anúncio fora de sequência que resultou em uma duração de conteúdo principal negativa.

* Zendesk nº 20522: Não é possível ignorar anúncios VPAID 2.0

**Observação**: Esse problema requer o player do Flash 21.0.0.182 ou posterior.

* Esse problema foi resolvido ao ignorar os anúncios VPAID durante o perdão do anúncio.
* Quando a política adbreak está definida para ignorar, os eventos de ad break ainda são despachados. O estado do player está inconsistente.

Esse problema resolveu se comportar corretamente e não despachar eventos quando o ad break é ignorado.

* Zendesk #20955 Definir pares de valores chave na propriedade customParameters por meio do gerador de oportunidade

**Observação**: Esse problema requer o player do Flash 21.0.0.182 ou posterior.

A Solicitação de Auditude analisa as AuditudeSettings para parâmetros personalizados ao criar uma unidade de anúncio para solicitações de publicidade.

Esse comportamento foi alterado para incluir parâmetros personalizados do objeto Oportunity na solicitação. Além disso, várias oportunidades com parâmetros personalizados diferentes não podem ser preenchidas em uma solicitação do Auditude.

* O Zendesk #21227 - m3u8 não é reproduzido de forma consistente

**Observação**: Esse problema requer o player do Flash 21.0.0.211 ou posterior.

Esse problema foi resolvido permitindo que o TVSDK ignorasse o manifesto (subperfis HLS) que contém o codec AC3 que o TVSDK não suporta (surround).

**Versão 1.4.20**  (762)

* Zendesk #19181 - Trick play fast forward to live point trava o stream.

**Observação**: Esse problema requer o player do Flash 20.0.0.306 ou posterior.

* Zendesk #19286 - Falha do Flash Player ao buscar para frente e para trás em um fluxo FER.

**Observação**: Esse problema requer o player do Flash 20.0.0.306 ou posterior.

As falhas ocasionais que ocorreram ao buscar no Google Chrome foram resolvidas ao encerrar as consultas, se as consultas demorarem muito para obter uma resposta ou se o soquete estiver sendo desligado.

* Zendesk #19305 - Reprodução com cópia encontrada ao reproduzir um fluxo com descontinuidades A/V.

**Observação**: Esse problema requer o player do Flash 20.0.0.306 ou posterior.

Esse problema foi resolvido através do relatório de um aviso.

* Zendesk # 19359 - Flash Player travado devido à posição de #EXT-X-FAXS-CM: no manifesto de nível de conjunto.

Esse problema foi resolvido quando a tag #EXT-X-FAXS-CM era exibida na lista de reprodução superior antes da taxa de bits individual ou dos segmentos na lista de reprodução.

* Zendesk #19489 - Fast Forward to Live Point paralisa o plug-in (stream ao vivo)

Esse problema é o mesmo do Zendesk nº 19181.

* Zendesk #19699 - TVSDK falha ao alternar entre as faixas de legendas WebVTT

Esse problema foi resolvido fazendo o despejo do reprodutor e recarregando o manifesto quando um rastreamento é alterado e corrigindo o problema de conversão da string UTF8 que afetou os nomes de rastreamento da legenda WebVTT de byte duplo.

**Versão 1.4.19**  (1.4.19.738)

* Zendesk #18234 - Flash Player falha ao reproduzir os fluxos com strings Unicode no CC

Esse problema requer o Flash Player FP 20.0.0.267 ou posterior e foi resolvido manipulando a sequência de caracteres Unicode corretamente.

* Zendesk nº 18304 - Suporte de integridade de fluxo para anúncios VPAID

Esse recurso exige o Flash Player FP 20.0.0.267 ou posterior e foi introduzido na versão 1.4.19.

* Zendesk #18766 - O reprodutor de referência não consegue exibir caracteres unicode não latinos em nomes de rastreamento CC

Esse recurso requer o Flash Player FP 20.0.0.267 ou posterior e foi corrigido manipulando corretamente a sequência de caracteres Unicode.

* Zendesk #18804 - Falha do reprodutor no Firefox 42

Esse problema requer o Flash Player FP 20.0.0.235 ou posterior e é o mesmo problema do Zendesk nº 18723.

* Zendesk nº 18864 - Falha do plug-in completo do Flash Player

Esse problema requer o Flash Player FP 20.0.0.235 ou superior e é igual ao Zendesk nº 18723.

* Zendesk #18998 - Se os carimbos de data e hora de áudio e vídeo não corresponderem, ocorrerá um download infinito de segmentos em descontinuidade.

Esse problema foi resolvido ao ignorar a lacuna entre os carimbos de data e hora e apenas reproduzir o conteúdo baixado.

* Zendesk #19093 - Mid-roll ads só podem ser vistos uma vez com conteúdo de reprodução de evento completo e ao vivo (FER), mas esses anúncios não podem ser vistos novamente quando o encaminhamento ou a busca dos anúncios forem rápidos

No seletor adPolicy padrão do Primetime, se um anúncio intermediário for assistido, o adBreak não será movido para a posição procurada ao concluir uma busca. Para reproduzir o anúncio novamente, após a busca, o aplicativo precisa substituir a função selectAdBreaksToPlay() .

* Zendesk #19101 - Rebobinar em anúncios intermediários não resolvidos remove o posicionamento do anúncio.

Esse problema foi resolvido permitindo que o reprodutor atualizasse o tempo de playbackMetrics, o MinimumOpportunityTime e a Linha do tempo.

* Zendesk #19102 - Problemas com o modo FER e trick

Esse problema requer o Flash Player FP 20.0.0.267 ou posterior e foi resolvido definindo o advertisingMetadata.adSignalingMode corretamente.

* Zendesk #19175 - Algumas vezes os anúncios de pré-lançamento não são exibidos na primeira vez que o fluxo é reproduzido.

Esse problema foi resolvido adicionando uma nova API, adRequestTimeout, ao AuditudeSettings de um tempo limite de solicitação de anúncio. Agora os usuários podem substituir o tempo limite padrão da solicitação de anúncio dos 10 anos.

**Versão 1.4.18**  (1.4.18.722)

* Zendesk #3324 - Os relatórios de anúncios do Primetime não rastreiam ad breaks quando não há mídia de anúncio em um VMAP.

Quando um ad break está vazio, o início e a conclusão dos eventos de rastreamento do ad break não eram ping. Esse problema foi resolvido enviando pings de início de ad break em ad breaks vazios, como VMAP AdBreak, com um nó AdSource válido.

**Versão 1.4.17**  (1.4.17.702)

* Zendesk #17168 - As legendas não aparecem por 10 segundos ou mais depois de alternar a visibilidade

Esse problema foi resolvido fornecendo suporte para a tag EXT-X-MEDIA-TIME para arquivos de legenda vtt.

* Zendesk #17983 - A falha no download de qualquer chave para um manifesto faz com que toda a reprodução do manifesto falhe

**Observação**: Você deve ter pelo menos Flash Player FP 19.0.0.245 ou superior.

Às vezes, ao reproduzir conteúdo ao vivo, pode haver chaves inválidas no manifesto (por exemplo, para períodos de blecaute), mas outros intervalos de tempo podem ter chaves válidas e ainda serão reproduzidos. Anteriormente, quando uma chave que estava listada em um manifesto não podia ser baixada, o manifesto inteiro falhava. Agora, o manifesto falha somente quando todas as chaves listadas não podem ser baixadas. Se algumas chaves forem válidas, mas algumas dessas chaves não puderem ser baixadas, o conteúdo será reproduzido. Ainda falharemos se tentarmos reproduzir um segmento que requer uma chave que não temos.

* Zendesk #18554 - Stream Integrity eliminando os cookies em alguns casos

**Observação**: Você deve ter pelo menos Flash Player FP 19.0.0.245 ou superior.

Correção de um bug no código de manipulação de cookies que poderia truncar valores de cookies.

**Versão 1.4.16**  (1.4.16.684)

* Zendesk # 3732 - Adicionar suporte para proxies no Chrome para Integridade de Fluxo (requer Flash Player FP 19.0.0.207 ou superior)

Este é um aprimoramento.

* Zendesk nº 4244 - Problemas de transmissão na rolagem do PTS

Esse problema foi resolvido detectando sobreposições e gerenciando a descontinuidade por tipo de carga, e não genericamente.

* Zendesk nº 4487 - Rastreamento do canal linear de conteúdo

Esse problema foi resolvido reinicializando o rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17427 - Integridade de fluxo do Adobe que não funciona por meio de um proxy no Chrome (Win7) ()

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

Esse problema é o mesmo do Zendesk nº 3732.

* Zendesk #17907 - Atraso no Live Stream do HLS com Flash Player 19

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

Esse problema foi resolvido com a manipulação dos fluxos ao vivo, onde os domínios dos arquivos TS são alterados ao recarregar o manifesto ao vivo, e os arquivos são baixados duas vezes.

* Zendesk #17931 - Falha na reprodução do conteúdo HLS com tabulação no início

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com a manipulação de fluxos sem áudio nos primeiros 2 segundos do primeiro arquivo TS.

* Zendesk #17934 - Live Streaming Failure with Flash 19.0.0.185

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com a manipulação de fluxos ao vivo com intervalos de tempo entre quadros de áudio e vídeo nos limites do segmento.

* Zendesk #17973 - Última falha do Flash Player 19.0.0.185 durante a exibição

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com a manipulação de áudio sem mudo com inserção de anúncio intermediário. (A opção de analisador ocorre e, em qualquer ponto da reprodução, o conteúdo é transferido para o anúncio intermediário, ou no meio da reprodução do anúncio, e assim por diante).

* Zendesk #18049 - Flash 19 crash com Firefox 42 beta

Esse problema é o mesmo do Zendesk nº 17973.

**Versão 1.4.15**  (1.4.15.678)

* Zendesk nº 4377: Acione o evento AD_BREAK_SKIPPED ao ignorar um ad break por causa da política de anúncios.

A correção era adicionar AD_BREAK_SKIPPED se um anúncio fosse ignorado.

* Zendesk nº 4496 - Integridade do fluxo: Erro 102100 com redirecionamentos para fluxos com token.

A correção foi adicionar suporte para a configuração da propriedade AVNetworkConfiguration useCookieHeaderForAllRequests por meio do TVSDK.

* Zendesk #17179 - Reprodutor de Flash travando em várias alterações do SAP para conteúdo criptografado.

Correção de uma falha durante a reprodução de algum conteúdo criptografado.

**Observação**: A correção requer o Flash Player 19.0.0.200 ou superior.

* Zendesk #17499 - como não removemos os midrolls após o relógio, mas removemos as permissões do conteúdo fer

Adição de um tipo a AdBreakTimelineItem (AdBreakTimelineItem.placementType) para que AdPolicySelector possa retornar uma política diferente para conteúdo precedente, intermediário e posterior.

* Zendesk # 17665 - Limitação da largura de banda

A correção era remover a lógica de alterar o tamanho do buffer de destino para o tamanho do buffer inicial quando o buffering começasse.

**Versão 1.14.14**  (1.4.14.771)

* Zendesk #17363 - Corrigir documentação README para o reprodutor de referência

   * Esclareça as instruções para baixar e instalar o playerglobal.swc.
   * Adicione instruções para atualizar a configuração do projeto com uma versão específica do flash player.
   * Atualize a configuração do projeto AdvertisingOverlay para usar a versão mínima do player.
   * Atualizar a configuração do projeto ReferenceCore para usar o reprodutor específico versão 11.9

* Zendesk #17471 - Congelamentos do reprodutor

Correção parcial de um problema em que um anúncio não é reproduzido do início após a busca.

* Zendesk #17496 - Podbuster não é resolvido ao buscar de volta na janela do DVR

Forneça parâmetros personalizados para cada ad break.

**Versão 1.4.13**  (1.4.13.660)

* Zendesk #4037 - No Useable Profile Error (requer o Flash Player 18.0.0.232 ou superior)

corrija o problema de análise do url quando o parâmetro de consulta contiver &quot;http&quot;

* Zendesk #4260 - Flash Player 18 falha no IE11 (requer o Flash Player 18.0.0.232 ou superior)

Correção de uma falha ao reproduzir vídeo no modo de tela cheia com o IE11

* Zendesk #4262 - Adobe Primetime player falha no Windows 10 (requer o Flash Player 18.0.0.232 ou superior)

Correção de uma falha ao reproduzir vídeo no modo de tela cheia com o FireFox no Windows.

* Zendesk #4279 - HLS TVSDK adição inserção -302 problema de redirecionamento no iOS e no desktop

Correção de um problema em que um URL não era reconhecido corretamente porque não tinha extensão

* Zendesk # 4306 - Falha do Flash Player ao acessar a tela cheia somente no Win (requer o Flash Player 18.0.0.232 ou superior)

Correção de uma falha ao reproduzir vídeo no modo de tela cheia no Windows.

* Zendesk #4480 - Missing ID3 tag events (requer o Flash Player 18.0.0.232 ou superior)

**1.4.12 **(1.4.12.656)

* Zendesk nº 2751 - CSAI e CRS | Reforçar: Manipule elementos dinâmicos em determinados URLs de arquivo de mídia.

Serviço de reempacotamento criativo atualizado para lidar corretamente com anúncios com URLs criativos dinâmicos.

* PTPLAY - 2114 - Suporte à reprodução MP4.

A reprodução básica de conteúdo MP4 agora é compatível, incluindo reprodução, pausa e busca.

O seguinte requer o Flash Player 18.0.0.225 ou superior:

* Zendesk #3992 - Velocidades adicionais do TrickPlay.

O TrickPlay agora aceita taxas maiores que 16x: +/- 32, +/-64 e +/-128.

* Zendesk # 3113 - Falha do plug-in do Flash Player

Correção de uma falha ao tentar reproduzir um anúncio de redirecionamento no Mac Firefox.

* Zendesk #4037 - Sem erro de perfil utilizável
* Zendesk #4262 - Adobe Primetime player falha no Windows 10

Correção de uma falha no Windows Firefox durante a reprodução em tela cheia.

**Versão 1.4.11**  (1.4.11.648)

* Zendesk #1869 - Issue Changing Font Size (requer o Flash Player 18.0.0.200)

Permitir que tamanhos de legenda sejam usados no código de legenda WebVTT.

* Zendesk #3113 - Flash Player Plugin Crashing (requer o Flash Player 18.0.0.200)
* Zendesk nº 3268 - Desktop: O reprodutor de vídeo inicia a cintilação após +- 40/50 segundos e começa a ficar preto após +- 90 segundos (requer o Flash Player 18.0.0.200)

Correção do bug do vídeo do estágio.

* Zendesk # 3670 - Erro INVALID_PARAMETER no VOD ao buscar no reprodutor de referência (requer o Flash Player 18.0.0.200)

InvalidateProfiles no ThreadSeek quando um novo período é detectado.

* Zendesk #3896 - Flash Player crash with Stream Integrity set to ON on Chrome (requer Flash Player 18.0.0.200)

Correção de uma falha no modo de rede nativo no pimenta

* Zendesk #3905 - O reprodutor TVSDK não carrega quando hospedado no CDN

Correção de problemas que localizavam o token curinga quando o pageDomain era diferente do domínio swf.

**Versão 1.4.10**  (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player trava Flash no Firefox

Correção de uma falha ocasional de Flash Player com o Firefox no Mac quando um fluxo, reproduzido em um monitor externo, alternava para um fluxo de taxa de bits mais alto.(requer o Flash Player 18.0.0.160)

* Zendesk nº 3268 - Desktop: O reprodutor de vídeo inicia a cintilação após `+-` 40/50 segundos e começa a ficar preto após `+-` 90 segundos

Correção de um problema no Mac Chrome, em que o fluxo começava a cintilar e eventualmente ficava preto. (requer o Flash Player 18.0.0.161)

* Zendesk #3304 - macro VAST 3.0 `[ERRORCODE]` não sendo preenchida

   * o código de erro 400 será exposto se o anúncio em linha apresentar anúncios com conteúdo incorreto.
   * `[ERRORCODE]` macro será codificada no URL

* Zendesk # 3601 - Solicitação de aprimoramento: Gerenciamento complementar de invólucro

   * O TVSDK exibirá o companheiro de wrappers que contém recursos (html, iframe ou estático ) próximos ao embutido. (se o item em linha não contiver um para esse tamanho)
   * Os invólucros são complementares de recursos, a menos que sejam usados para exibição, serão ignorados. (não use para rastreamento )
   * Somente os companheiros de wrapper com recurso NO serão usados para fins de rastreamento. ( companheiro de wrapper que contém apenas rastreamento )

**Versão 1.4.9**

* Zendesk nº 2615 - problema ao remover a exibição do HLS da tela do desktop

Método clearVideo() adicionado ao MediaPlayer. Apaga o quadro de vídeo exibido, limpando o AVStream do objeto StageVideo. Só deve ser chamado se o vídeo estiver pausado, e replaceCurrentResource ou replaceCurrentItem deve ser chamado antes que play() possa ser chamado novamente.

* Zendesk #3169 - Atualizar reprodutor de referência com integração com o Adobe Analytics

O reprodutor de referência foi atualizado com a integração do Adobe Analytics

* Zendesk # 3296 - Desktop HLS TVSDK - Anúncios de terceiros VAST que não são reproduzidos

os tipos mime para o formato HLS diferenciavam maiúsculas de minúsculas, isso estava incorreto e foi alterado para que não distinguissem mais maiúsculas de minúsculas

**Versão 1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000 (requer o Flash Player 17.0.0.184)
* Zendesk # 3007 - Anúncios precedentes que não apareciam após a atualização para o Flash Player 17 (requer o Flash Player 17.0.0.184)
* Zendesk #3085 - Desktop HLS Player Throws 106000 Error after 60 seconds (requer o Flash Player 17.0.0.184)

**Versão 1.4.7**

* Zendesk #2760 - DISCONTINUITY tag ignorada durante o modo TrickPlay (requer o Flash Player versão 17.0.0.158)
* Zendesk #2760 - DISCONTINUITY tag ignorada durante o modo TrickPlay (requer o Flash Player versão 17.0.0.158)

**Versão 1.4.6**

* Zendesk #2652 - Documentação de Auditude para HLS de desktop, Clarified Auditude media_id para documentação de HLS de desktop

**Versão 1.4.5**

* Zendesk #2256 - Access to Principal Playlist, PSDK atualizado para despachar eventos timedMetadata para tags assinadas na lista de reprodução principal. (requer o Flash Player versão 17.0.0.134)
* Zendesk #2417 - Player try tentar baixar legendas antes do início da reprodução, WebVTT estava usando a variável de número de segmento errada para correspondência de números de segmento. Bug só seria exibido para mídia com índices de segmento a partir de zero. (requer o Flash Player versão 17.0.0.134)
* Zendesk #2537 - Flash player trava ao usar o plug-in de pimenta com o Chrome (requer Flash Player versão 17.0.0.134)
* Zendesk #2547 - Legendas árabes: O texto deve ser alinhado, justificado à direita (requer Flash Player versão 17.0.0.134)

**Versão 1.4.4**

* Zendesk nº 1561 - Re: `[Adobe Primetime]` Atualização: Suporte a failover baseado no cliente HLS para PROGRAM-DATE-TIME no Desktop PSDK (requer o Flash Player versão 16.0.0.305 ou superior)
* Zendesk #2197 - `[Ads]` Rastreamento de erros de anúncio
* Zendesk nº 2286 - Solicitação de recurso: Forneça informações sobre o status de carregamento do anúncio (VPAID)
* Zendesk nº 2285 - Solicitação de recurso: Ignorar anúncio após uma duração de tempo limite especificada
* Bug #3921755 - Atualização da biblioteca OpenSSL para a versão 1.0.1L no Flash Player (requer Flash Player versão 16.0.0.305 ou superior)

**Versão 1.4.2**

* Zendesk #1303 - Vertical Offset for Closed Caption (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento esperada: (dezembro de 2014)
* Zendesk #1870 - Closed Caption On &amp; Off (Legenda oculta ativada e desativada) (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento esperada: (dezembro de 2014)
* Zendesk #2110 - A reprodução fica presa após tentar entrar na tela cheia durante um anúncio VPAID (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento esperada: (dezembro de 2014)
* Zendesk #2199 - `[VPAID]` Player não responde ao buscar anúncios anteriores
* Zendesk nº 2358 - Re: `[Analytics]` Dados de capítulo incorretos

**Versão 1.4.1**

* Atualização da API de blecautes para ser consistente com a implementação de Android e iOS.

**Versão 1.4.0**

* Zendesk #1024 - Recurso para remover anúncio do fluxo por meio do manifesto
* Zendesk #1423 - A falha de reprodução de HLS está travando o Flash Player (sem erro relatado)
* Zendesk #1674 - ClosedCaption Not displayed, Corrija a exibição da legenda 708 quando os códigos ETX 0x03 estiverem ausentes.

## Problemas conhecidos {#known-issues}

* As Legendas ocultas não funcionarão com conteúdo somente áudio, pois o sistema de legendas precisa de vídeo para funcionar.
Sem vídeo, não há dimensão do visor e sem uma dimensão do visor, não é possível exibir gráficos de legendas.
* A integridade do fluxo é um pouco mais lenta no Google Chrome devido às restrições da sandbox Chrome.
* No TVSDK 1.4, se você desativar o autoPlay, um erro de DRM pode ocorrer quando o reprodutor permanece inativo por pelo menos um minuto. Para contornar esse problema, ao desativar o autoPlay, mas pré-carregar ativos, modifique `ReferenceCore.as` alterando o conteúdo de `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versão 1.4.13** PTPLAY-8501 - Quando o VMAP retorna dois anúncios MP4 diretos não transcodificados, o mesmo fallback é reproduzido duas vezes.

* **Versão 1.4.2** Na versão 16 do Flash Player, um problema foi identificado com a lógica de &quot;desativação&quot; do ABR, depois que o reprodutor entra em um evento de buffer vazio. O problema impede que a taxa de bits seja reduzida em ambientes de largura de banda inválidos, uma vez que o reprodutor entra em um estado de buffering. Para contornar o problema, faça com que seu aplicativo defina `BufferControlParameters.initialBufferTime` como `BufferControlParameters.playbackBufferTime` temporariamente durante o estado de buffering (ou seja, em um evento `BufferEvent.BUFFERING_BEGIN`) e redefina-o para os valores definidos no evento `BufferEvent.BUFFERING_END`. A correção para esse problema estará disponível na próxima versão de patch do Flash Player versão 16.

* **Versão 1.4.0**

   * PTPLAY-1634 - A mesma tag Subscribed tem diferentes carimbos de data e hora em diferentes janelas ativas. Quando as janelas em tempo real são movidas, a mesma tag em cada uma delas deve ter os mesmos carimbos de data e hora. No entanto, às vezes, as mesmas tags têm carimbos de data e hora diferentes.
   * PTPLAY-28 - A linha do tempo do MediaPlayer não inclui quebras vazias.
   * Um arquivo de política entre domínios (cross-domain.xml) é necessário para permitir o fluxo de conteúdo de um domínio diferente. [Configurar um arquivo cross-domain.xml para transmissão HTTP](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html).
   * Bug #3694203 - Em um fluxo de DVR, a busca dentro de um intermediário de reprodução em outro anúncio intermediário pode levar ao congelamento do navegador
   * Bug #3753725 - selectPolicyForSeekIntoAd não leva em conta se o ad break foi observado
   * Bug #3754529 - Os anúncios precedentes não são removidos do stream ao buscar de volta em um stream DVR ao vivo
   * Bug #3761896 - Se a busca for permitida durante a reprodução do anúncio, os marcadores de anúncio serão reajustados após a busca. A solução alternativa é não usar o retorno de chamada ITEM_UPDATED durante a busca
   * Bug #3779889 - A chamada completa não é feita ao atingir o fim da reprodução de truque no Video Analytics
   * Bug #VA-779 - A pulsação do evento de alteração da taxa de bits não é enviada para a Análise de vídeo aprimorada com implementação de referência de suporte do Heartbeat - A reprodução do truque não é implementada no aplicativo de amostra.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
