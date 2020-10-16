---
title: Notas de versão do TVSDK 1.4 para Desktop HLS
seo-title: Notas de versão do TVSDK 1.4 para Desktop HLS
description: As Notas de versão do TVSDK for Desktop HLS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no TVSDK DHLS.
seo-description: As Notas de versão do TVSDK for Desktop HLS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no TVSDK DHLS.
uuid: 84da27b7-299b-478d-88f5-ef943f0a8321
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: e4437a26-9454-4da1-ae87-0fce664aac3d
translation-type: tm+mt
source-git-commit: ba291a4615a8e0713cf610f76f41e328da96ec4d
workflow-type: tm+mt
source-wordcount: '5222'
ht-degree: 0%

---


# Notas de versão do TVSDK 1.4 para Desktop HLS {#tvsdk-for-desktop-hls-release-notes}

As Notas de versão do TVSDK for Desktop HLS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no TVSDK DHLS.

## Novos recursos {#new-features}

**1.4.31**

* **Suporte a vários CDN para anúncios de CRS**

   * Por padrão, todos os ativos transcodificados serão hospedados no CDN de propriedade do Adobe no Akamai. Com a versão mais recente, o Adobe Creative Repacking Service (CRS) fornece a capacidade de carregar os criativos transcodificados em vários CDNs, conforme especificado pelo cliente.
   * Novas APIs são adicionadas ao TVSDK para permitir a especificação do url criativo do CRS final quando o URL padrão não é usado. Consulte a documentação para saber como usar essas novas APIs.

### Novos recursos das versões anteriores {#new-features-previous}

**1.4.30**

* **Métricas de faturamento**

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

**1.4.24**

* **Conexão de rede persistente**

Importante: Você deve ter pelo menos Adobe Flash Player versão 22 ou posterior instalado.
Conexões de rede persistentes criam e armazenam uma lista interna de conexões de rede que podem ser reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede. As conexões de rede persistentes devem aumentar a eficiência e diminuir a latência no código de rede.

Nesta versão, esse recurso não é compatível com o Apple Safari e o Mozilla Firefox em um Mac.

**1.4.19**

* Suporte à integridade de fluxo para anúncios VPAID.
* Ativada a opção de guia Silenciar no player do Flash FP 20.0.0.267 para Firefox 42 e posterior, corrigindo o problema de travamento.

**1.4.18**

* O Primetime Desktop HLS TVSDK agora é compatível com as criações de SWF linear VPAID 2.0 para permitir uma experiência avançada de anúncios interativos em fluxo.

**1.4.10**

* **Ad Fallback, Encadeamento gradual na lógica de seleção de anúncio (Zendesk #3103)** Para anúncios VAST (criativos) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Anúncio de fallback para anúncios](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)VAST e VMAP.

**1.4.8**

* **Biblioteca do Video Heartbeats (VHL) atualizada para a versão 1.5**

   * Capacidade de enviar metadados com start de vídeo e/ou start de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - As pulsações são menores em média e menores em tamanho.

**1.4.7**

* **Suporte para individualização no local**

Suporte para instalações no local do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para acessar um terminal diferente.

**1.4.6**

* **Criptografia AES de amostra (requer a versão 17.0.0.134 do Flash Player)**

A criptografia AES baseada em amostra agora é compatível.

**1.4.2**

* **Atualização da Biblioteca do Video Heartbeats (VHL) para a versão 1.4.0.1**

   * Adicionada a capacidade de agrupar diferentes casos de uso de análises, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete. A quebra de anúncio é inferida das chamadas de método trackAdStart e trackAdComplete.
   * A propriedade playhead não é mais necessária ao rastrear anúncios.

**1.4.0**

* **Sinalização de Blecaute com Substituição** de Conteúdo Alternativa Como parte da atualização 1.4 do TVSDK, o TVSDK também oferece suporte para entrar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remova/substitua anúncios** C3 Agora, nenhum trabalho de preparação adicional é necessário para inserir dinamicamente novos anúncios nos ativos VOD (Video-on-demand) que saem da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova funcionalidade poderosa também é útil em casos em que o conteúdo ao vivo/linear é exibido durante a transmissão e é imediatamente suspenso para uso como conteúdo sob demanda sem tempo adequado para &quot;limpar&quot; o ativo.

## Problemas resolvidos {#resolved-issues}

>[!NOTE]
>
>Todos os clientes TVSDK que usam CRS são altamente incentivados a atualizar para pelo menos TVSDK 1.4.32 no iOS, Android e Desktop HLS. Essa atualização será uma substituição instantânea da implementação do aplicativo existente. Após a atualização, verifique as solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo, Charles) para verificar se a versão no caminho reflete a versão 3.1. Por exemplo,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versão 1.4.41**

* Zendesk #33777 - Localhost token SWF para compilação de distribuição DHLS expirado.

   Atualização do token localhost para demonstração PMP no DHLS.

### Resolvidos problemas nas versões anteriores {#resolved-issues-previous}

**Versão 1.4.38** (891)

* Zendesk #30731 - O TVSDK não reproduz vários anúncios VPAID em um AdBreak.

   Corrigida a reprodução de vários anúncios VPAID em um AdBreak.

* Zendesk #29968 - Billboard do Duplo.

   O player de vídeo pode repetir o último segmento de um período em que ocorre um switch ABR. Devido a isso, às vezes o último segmento de pré-rolagem se repetia. Isso foi corrigido.

**Versão 1.4.35** (879)

* Zendesk #26058 - Suporta eventos VPAID nativos

**Versão 1.4.33** (873)

* Zendesk #21701 - Envia o URL criativo original para a solicitação CRS 1401 em vez do url normalizado.

   O problema em que URLs já reempacotados estão sendo solicitados para transcodificação foi corrigido, conforme exigido pelo back-end do CRS.
* Zendesk #26197 - Compactação anamórfica não reproduzida na resolução de exibição desejada.

   **Observação**: Esse problema requer o player de Flash 24.0.0.194 ou posterior.

   Foi corrigido o problema em que entradas ausentes nas tabelas de proporção eram usadas para calcular a largura de saída.

* Zendesk #26840 - Falha na detecção HDCP no IE11 + Windows7 após segunda tentativa.

   **Observação**: Esse problema requer o player de Flash 24.0.0.218 ou posterior.

   Esse problema foi solucionado modificando o processamento da fila de mensagens principal do AdobeCP para iterar por toda a fila, em vez de apenas bloquear a primeira mensagem.

* Zendesk #27460 - A nova conta do Akamai não consegue lidar com uma solicitação de CDN de POST.

   A nova conta CDN não consegue processar uma solicitação de CDN POST. Esse problema foi resolvido atualizando o código para fazer com que a solicitação de anúncio cdn.auditude.com fosse GET em vez de POST.
* Zendesk #27619 - travamento do Flash no Windows 10

   **Observação**: Esse problema requer o player de Flash 24.0.0.218 ou posterior.

   Esse problema foi resolvido evitando uma falha como resultado de URLs longos.

* Zendesk #28218 - O evento de rastreamento não é acionado enquanto o plackback é disparado do ponto de retomada

   Esse problema é o mesmo da Zendesk nº 26592. Foi corrigido o problema em que as operações de busca eram permitidas quando o player de mídia estava no estado PREPARADO para fluxos VOD.

**Versão 1.4.32** (867)

* O evento de rastreamento do Zendesk #26592 não é acionado quando a reprodução é start a partir do ponto de retomada

O código não atualizava o item de quebra de anúncio precedente quando o ponto de retomada não era zero. Esse problema foi resolvido adicionando lógica para atualizar o código quando os tempos de start do intervalo não correspondem.

* Zendesk #27022 Os anúncios não são reproduzidos na segunda vez que um ativo é reproduzido

As exceções com os métodos de matriz foram corrigidas.

**Versão 1.4.30** (855)

Os seguintes problemas foram resolvidos para o TVSDK nesta versão:

* Zendesk #22898 - Legendas ausentes não devem causar falha na reprodução.

**Observação**: Esse problema requer o player de Flash 23.0.0.185 ou posterior.

Esse problema foi resolvido permitindo que o TVSDK continuasse a reprodução, mesmo se o manifesto não tivesse o WebVTT M3U8, e registrasse apenas um aviso.

* Zendesk #23454 - Anúncios de terceiros (VPAID) não são tratados corretamente

Esse problema foi resolvido com o manuseio correto de anúncios VPAID com base em IDs de conteúdo em vez de intervalos de tempo.

* Zendesk #24528 - Métricas de uso do TVSDK para faturamento.

Importante: Esse problema requer o player de Flash 23.0.0.185 ou posterior.

* Problema de legenda fechada no Zendesk # 25432 durante o redimensionamento do player.

Importante: Esse problema requer o player de Flash 23.0.0.185 ou posterior.

O código do mapa de textura de exibição da legenda foi corrigido para lidar corretamente com as coordenadas durante o redimensionamento do player.

A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

* Zendesk #23730 - As métricas de taxa de bits estão vazias

Esse problema foi solucionado rastreando as alterações na taxa de bits no VideoAnalyticsTracker.

* Adicionada uma nova API, assetDuration, ao PTVideoAnalyticsTrackingMetadata para atualizar a duração do ativo para fluxos ao vivo/linear.

**Versão 1.4.28** (848)

* Zendesk #25027 - Auditude não funciona na versão 1.4.27 para desktop

Esse problema foi resolvido com a adição do código para verificar o AUDITUDE_METADATA_KEY e a troca entre AUDITUDE_METADATA_KEY e ADVERTISING_METADATA_KEY.

* Zendesk #24428 - Problema de buffering frequente usando TVSDK para reproduzir um HLS DRM

Esse problema foi resolvido levando-se em conta que, quando não há configuração de anúncio, o TVSDK pode acelerar o processamento, eliminando a retenção de anúncio precedente e a retenção de reserva ativa na linha do tempo projetada para sincronizar a inserção de anúncio.

* Zendesk #24344 - Desativar arquivos WebVTT para melhorar o tempo de start.

**Observação**: Esse problema requer o player de Flash 23 ou posterior.

Esse problema foi resolvido ao carregar os arquivos WebVTT somente quando as legendas precisam ser exibidas.

* Zendesk #24994 - As legendas ocultas são descartadas do player ao retornar do intervalo comercial

**Observação**: Esse problema requer o player de Flash 23 ou posterior.

O código EOC espúria fazia com que a exibição da legenda desaparecesse. Esse problema foi resolvido forçando os códigos de 608 legendas RU2, RU3 e RU4 a fornecerem a visibilidade correta na janela ativa atual.

**Versão 1.4.27** (844)

* Zendesk #21554 - Beacons de erro TVSDK não acionados para tipo de aplicativo = video/mp4

Esse problema foi solucionado ao permitir que o TVSDK faça ping nos URLs de rastreamento de erros corretos em formatos de ativos inválidos.

* Zendesk #23402 - Reprodução de anúncio incompleta

**Observação**: Esse problema requer o player de Flash 23 ou posterior.

Após receber um erro 404 em determinadas solicitações, uma falha pode ocorrer. Esse problema foi resolvido garantindo que a conexão não seja desligada enquanto a resposta estiver sendo tratada. A resolução garante que os arquivos de anúncio VPAID não sejam contados incorretamente, de modo que não sejam liberados durante o download.

* Zendesk #23621 - Retry is failure on 400 and 404 (Falha na tentativa 400 e 404)

**Observação**: Esse problema requer o player de Flash 23 ou posterior.

Correção do problema que causava a corrupção de metadados DRM ao alternar entre perfis diferentes.

* Zendesk #23705 - Anúncios de vídeo congelando durante quebras de linha

**Observação**: Esse problema requer o player de Flash 23 ou posterior.

Esse problema é o mesmo da Zendesk nº 23621.

* Zendesk #23905 - Algumas pausas de anúncio pulam em pausas de anúncio

**Observação**: Esse problema requer o player de Flash 23 ou posterior.

O código de rede nativo do Windows foi corrigido para garantir que as conexões não fechem alças que estão sendo usadas atualmente por outras conexões.

* Ticket #24029 - Os fluxos HLS FER não reproduzem todos os anúncios intermediários no arquivo .json mid-roll.

Esse problema foi resolvido permitindo que os clientes definissem parâmetros personalizados separadamente na instância Opportunity para que os clientes não precisassem substituir OpportunityGenerator.

**Versão 1.4.26** (839)

* Zendesk #18854 - Atualizar lógica de seleção criativa com base nas regras do CRS
   * Fornecido suporte para atualizar a lógica de seleção criativa com base nas regras do CRS

* Zendesk #22725 - playbackManager.beginPlayback() implementa no aplicativo de amostra para desktop

   * Corrigido ao remover esta chamada redundante no final de startPlaybackFromFlashVars, pois o método é chamado de setupVideo()

* Zendesk #22807 - Exceção de referência nula do SeekManager

   * Corrigido fornecendo a proteção necessária do ponteiro NULL dentro do SeekManager em relação a _dispatcher

* Zendesk #22822 - Buffering frequente ao usar TVSDK para reproduzir um HLS claro

   * Corrigida removendo a oportunidade inicial gerada por adSignalingModeOpportunityGenerator se não houver anúncio

* Zendesk #23378 - A integridade do fluxo bloqueia rules.xml

   * Correção ao carregar o arquivo rule.xml pelo fluxo de trabalho de integridade do fluxo

**Versão 1.4.24** (817)

* Zendesk #19851 - Quando o player se adapta a uma taxa de bits diferente, ele pula alguns quadros de volta no tempo na nova taxa de bits, tornando uma experiência estranha

**Observação**: Esse problema requer o player de Flash 22.0.0.175 ou posterior.

O problema no qual o adaptador DRM é redefinido após o download de uma pequena fração de um segmento não é restaurado corretamente foi resolvido.

* Zendesk #20784 - Analytics: Acionar conclusões de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido com a adição de uma API (trackVideoComplete) para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo LINEAR/LIVE.

As seguintes bibliotecas foram atualizadas:

* Zendesk #21643 - Anúncios VPAID não são reproduzidos na íntegra

   * Biblioteca do AdobeMobile para 4.10.0
   * Biblioteca VHL para 1.5.6
   * Biblioteca VHL-Nielsen para 1.6.7

Esse problema foi resolvido usando um visor de altura zero para preencher o estágio quando um anúncio VPAID está sendo reproduzido.

* Zendesk #22110 - Analytics: Adicione um campo h:sc:ssl às chamadas de rastreamento de pulsação

Os problemas relacionados ao SSL foram corrigidos e a biblioteca VHL usada no TVSDK foi atualizada para a versão mais recente.

* Zendesk #22608 - O vídeo mostra uma tela preta intermitentemente (requer o Flash Player 22.0.0.175 ou posterior)

Durante a taxa de bits adaptável, com o limite máximo de taxa de bits, o recarregamento do vídeo mostra uma tela preta intermitentemente, mesmo que o cliente veja as atualizações para posicionar, e o cliente se comporta como se estivesse reproduzindo o conteúdo.

**Versão 1.4.23** (809)

* Zendesk #2887 - Problema de omissão de anúncio posterior quando a lógica da Regra de anúncio é aplicada ao TVSDK

**Observação**: Esse problema requer o player de Flash 21.0.0.240 ou posterior.

O problema no qual os anúncios posteriores eram ignorados quando a lógica da regra de anúncio era aplicada ao TVSDK foi corrigido.

* Zendesk #19863 - Anúncio com arquivo de mídia VPAID descartado

Se um vasto anúncio em linha tiver vários arquivos de mídia com um anúncio VPAID sendo o primeiro, o anúncio em linha não será reproduzido para streams ao vivo. Esse problema foi solucionado ao selecionar um arquivo de mídia diferente.

* Zendesk #21021 - Ligação tardia de áudio que causa repetição de segmentos de áudio

**Observação**: Esse problema requer o player de Flash 21.0.0.240 ou posterior.

O problema de repetição de áudio foi corrigido.

* Zendesk #21125 - Retornar do live/linear e quebrar precocemente

**Observação**: Esse problema requer o player de Flash 21.0.0.240 ou posterior.

Esta versão oferece suporte para retornar de uma pausa de anúncio antes que a pausa de anúncio seja reproduzida até a conclusão. O retorno antecipado é indicado por meio de uma tag manifest personalizada.

* O áudio de ligação tardia do Zendesk # 21369 causa um tempo inconsistente

**Observação**: Esse problema requer o player de Flash 21.0.0.240 ou posterior.

O problema de repetição de áudio corrigido também corrigiu esse problema.

* Zendesk #21760, 20921 - Audio Video Desync on Seek (Dessincronização de vídeo de áudio em busca).

**Observação**: Esse problema requer o player de Flash 21.0.0.240 ou posterior.

O problema de repetição de áudio foi corrigido.

* Zendesk #22024 - Erro ao executar o TVSDK

Foi corrigido o problema em que o player de referência não reproduzia nenhum fluxo e lançava uma exceção ao start.

**Versão 1.4.22** (791)

* Zendesk #17580 - Erro de tempo de execução Primetime com código 3357

**Observação**: Esse problema requer o player de Flash 21.0.0.197 ou posterior.

Os erros aleatórios 3357 que ocorreram ao inicializar corretamente o deviceID quando storeVoucher() é chamado foram corrigidos.

* Zendesk #21334 - Valor de tempo limite de solicitação de anúncio TVSDK para solicitações de anúncios de terceiros

Nesta versão, o tempo limite de solicitação de anúncio global foi adicionado.

**Versão 1.4.21** (782)

* Zendesk #19580 TVSDK aguarda a conclusão do resolvedor de conteúdo antes de enviar `PTTimedMetadataChangedNotification` notificações

**Observação**: Esse problema requer o player de Flash 21.0.0.182 ou posterior.

Esse problema foi resolvido no Desktop Reference Player, fornecendo a capacidade de definir tags de Anúncio e adicionar um gerador de oportunidade personalizado que mostra como assinar dicas personalizadas e como processar essas dicas em um arquivo VOD.

* O Zendesk #20806 Anúncios mid-roll futuros na janela DVR não serão acionados após a troca de câmeras

**Observação**: Esse problema requer o player de Flash 21.0.0.182 ou posterior.

Esse problema foi resolvido com a atualização do aplicativo para definir _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) para desativar a inserção de anúncio precedente em uma troca PIP e, como resultado, nenhuma oportunidade de pré-rolagem é gerada.

Uma funcionalidade de classificação foi introduzida para corrigir o posicionamento fora de sequência do anúncio que resultava em uma duração negativa do conteúdo principal.

* Zendesk #20522: Não é possível ignorar anúncios VPAID 2.0

**Observação**: Esse problema requer o player de Flash 21.0.0.182 ou posterior.

* Esse problema foi resolvido ignorando os anúncios VPAID durante o perdão do anúncio.
* Quando a política adbreak estiver definida para ignorar, os eventos de quebra de anúncio e de anúncio ainda serão despachados. O estado do player é inconsistente.

Esse problema foi resolvido para se comportar corretamente e não despachar eventos quando o intervalo do anúncio é ignorado.

* Zendesk #20955 Definir pares de valores chave na propriedade customParameters por meio do gerador de oportunidade

**Observação**: Esse problema requer o player de Flash 21.0.0.182 ou posterior.

A Solicitação de Auditude analisa as AuditudeSettings para obter parâmetros personalizados ao criar uma unidade de anúncio para solicitações de publicidade.

Esse comportamento foi alterado para incluir parâmetros personalizados do objeto Oportunity na solicitação. Além disso, várias oportunidades com diferentes parâmetros personalizados não podem ser compactadas em uma solicitação do Auditude.

* O Zendesk #21227 - m3u8 não é reproduzido de forma consistente

**Observação**: Esse problema requer o player de Flash 21.0.0.211 ou posterior.

Esse problema foi resolvido permitindo que o TVSDK ignore o manifesto (subperfis HLS) que contém o codec AC3 que o TVSDK não suporta (surround).

**Versão 1.4.20** (762)

* Zendesk #19181 - Trick play fast forward to live point lock up stream.

**Observação**: Esse problema requer o player de Flash 20.0.0.306 ou posterior.

* Zendesk #19286 - Falha de Flash Player ao buscar para frente e para trás em um fluxo FER.

**Observação**: Esse problema requer o player de Flash 20.0.0.306 ou posterior.

Os travamentos ocasionais que ocorreram ao buscar no Google Chrome foram resolvidos ao desligar os query, se os query demorarem muito para obter uma resposta ou se o soquete estiver sendo desligado.

* Zendesk #19305 - Reprodução instável encontrada ao reproduzir um fluxo com descontinuidades A/V.

**Observação**: Esse problema requer o player de Flash 20.0.0.306 ou posterior.

Esse problema foi resolvido com relatórios aviso.

* Zendesk # 19359 - Flash Player travado devido à posição de #EXT-X-FAXS-CM: no manifesto de nível definido.

Esse problema foi resolvido quando a tag #EXT-X-FAXS-CM aparece na lista de reprodução superior antes da taxa de bits individual ou dos segmentos na lista de reprodução.

* Zendesk #19489 - Plug-in Fast Forward to Live Point Stalls (Fluxo ao vivo)

Este problema é o mesmo que Zendesk #19181.

* Zendesk #19699 - TVSDK falha ao alternar entre as faixas de legendas WebVTT

Esse problema foi resolvido fazendo o player descarregar e recarregar o manifesto quando um rastreamento é alterado e corrigindo o problema de conversão da string UTF8 que afetou os nomes de rastreamento da legenda WebVTT de duplo byte.

**Versão 1.4.19** (1.4.19.738)

* Zendesk #18234 - Flash Player falha ao reproduzir os fluxos com strings Unicode no CC

Esse problema exige o Flash Player FP 20.0.0.267 ou posterior e foi resolvido com a sequência de caracteres Unicode corretamente.

* Zendesk #18304 - Suporte de integridade de fluxo para anúncios VPAID

Este recurso exige o Flash Player FP 20.0.0.267 ou posterior e foi introduzido na versão 1.4.19.

* Zendesk #18766 - O Reprodutor de referência não pode exibir caracteres unicode não latinos em nomes de rastreamento CC

Esse recurso exige o Flash Player FP 20.0.0.267 ou posterior e foi corrigido manipulando corretamente a string Unicode.

* Zendesk #18804 - Travamentos do player no Firefox 42

Esse problema exige o Flash Player FP 20.0.0.235 ou posterior e é o mesmo problema do Zendesk nº 18723.

* Zendesk #18864 - Falha de plug-in completo do Flash Player

Esse problema exige o Flash Player FP 20.0.0.235 ou superior e é igual ao Zendesk nº 18723.

* Zendesk #18998 - Se os carimbos de data e hora de áudio e vídeo não correspondem, ocorre um download infinito de segmentos em descontinuidade.

Esse problema foi resolvido ignorando a lacuna entre os carimbos de data e hora e apenas reproduzindo o conteúdo baixado.

* Zendesk #19093 - Anúncios de mid-roll só podem ser vistos uma vez com conteúdo de reprodução de evento real (FER), mas esses anúncios não podem ser vistos novamente quando o encaminhamento for rápido ou quando a busca for além dos anúncios

No seletor adPolicy padrão do Primetime, se um anúncio intermediário for observado, o adBreak não será movido para a posição procurada quando você concluir uma busca. Para reproduzir o anúncio novamente, após a busca, o aplicativo precisa substituir a função selectAdBreaksToPlay().

* Zendesk #19101 - O rebobinamento em anúncios intermediários não resolvidos remove o posicionamento do anúncio.

Esse problema foi resolvido permitindo que o player atualizasse o tempo playbackMetrics, o mínimoOpportunityTime e a Linha do tempo.

* Zendesk #19102 - Problemas com o modo FER e truque

Esse problema exige o Flash Player FP 20.0.0.267 ou posterior e foi resolvido com a configuração correta de advertidamenteMetadata.adSignalingMode.

* Zendesk #19175 - Às vezes, os anúncios de pré-rolagem não são exibidos na primeira vez que o fluxo é reproduzido.

Esse problema foi resolvido com a adição de uma nova API, adRequestTimeout, às AuditudeSettings para um tempo limite de solicitação de anúncio. Agora, os usuários podem substituir o tempo limite padrão de solicitação de anúncio dos 10 anos.

**Versão 1.4.18** (1.4.18.722)

* Zendesk #3324 - O relatórios de anúncios do Primetime não rastreia quebras de anúncios quando não há mídia de anúncio em um VMAP.

Quando uma pausa de anúncio está vazia, o start de pausa do anúncio e os eventos de rastreamento completos não estavam sendo vinculados. Esse problema foi resolvido enviando start de quebra de anúncio em intervalos vazios de anúncios, como VMAP AdBreak, com um nó AdSource válido.

**Versão 1.4.17** (1.4.17.702)

* Zendesk #17168 - As legendas não aparecem por 10 segundos depois de alternar a visibilidade

Esse problema foi resolvido fornecendo suporte para a tag EXT-X-MEDIA-TIME para arquivos de legenda vtt.

* Zendesk #17983 - A falha no download de qualquer chave para um manifesto faz com que toda a reprodução do manifesto falhe

**Observação**: Você deve ter pelo menos Flash Player FP 19.0.0.245 ou superior.

Às vezes, ao reproduzir conteúdo ao vivo, pode haver chaves inválidas no manifesto (por exemplo, para períodos de blecaute), mas outros intervalos de tempo podem ter chaves válidas e ainda serão reproduzidos. Anteriormente, quando uma chave que estava listada em um manifesto não podia ser baixada, o manifesto inteiro falhava. Agora, o manifesto falha somente quando todas as chaves listadas não podem ser baixadas. Se algumas teclas forem válidas, mas não for possível baixar algumas dessas teclas, o conteúdo será reproduzido. Ainda falharemos se tentarmos tocar um segmento que requer uma chave que não temos.

* Zendesk #18554 - Stream Integrity aparando os cookies em alguns casos

**Observação**: Você deve ter pelo menos Flash Player FP 19.0.0.245 ou superior.

Foi corrigido um erro no código de manipulação de cookies que podia truncar valores de cookies.

**Versão 1.4.16** (1.4.16.684)

* Zendesk #3732 - Adicionar suporte para proxies no Chrome para Integridade de Fluxo (requer Flash Player FP 19.0.0.207 ou superior)

Isto é um reforço.

* Zendesk #4244 - Problemas de transmissão em sobreposição de PTS

Esse problema foi resolvido pela detecção da sobreposição e pelo gerenciamento da descontinuidade por tipo de carga, e não genericamente.

* Zendesk #4487 - Rastreamento do Canal linear do conteúdo

Esse problema foi resolvido reinicializando o rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17427 - Integridade de fluxo de Adobe que não funciona por proxy no Chrome (Win7) ()

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

Esse problema é o mesmo que o Zendesk nº 3732.

* Zendesk #17907 - Live Stream Atraso no pHLS com Flash Player 19

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

Esse problema foi resolvido com a manipulação de fluxos ao vivo, onde os domínios dos arquivos TS são alterados ao recarregar o manifesto ao vivo, e os arquivos são baixados duas vezes.

* Zendesk #17931 - Falha na reprodução do conteúdo HLS com slate no início

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com a manipulação de fluxos sem áudio nos primeiros 2 segundos do primeiro arquivo TS.

* Zendesk #17934 - Live Streaming Failure with Flash 19.0.0.185

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com a manipulação de fluxos ao vivo com intercalamento de tempo entre quadros de áudio e vídeo nos limites do segmento.

* Zendesk #17973 - Flash Player mais recente 19.0.0.185 travamentos durante o mid-roll

**Observação**: A resolução exige o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com a manipulação de áudio sem mudo com inserção de anúncio intermediário. (A opção de analisador ocorre e, em qualquer ponto da reprodução, o conteúdo transição para o anúncio intermediário, ou no meio da reprodução do anúncio e assim por diante.)

* Zendesk #18049 - Falha no Flash 19 com Firefox 42 beta

Este problema é o mesmo que Zendesk nº 17973.

**Versão 1.4.15** (1.4.15.678)

* Zendesk nº 4377: Dispare o evento AD_BREAK_SKIPPED ao ignorar uma pausa de anúncio devido à política de publicidade.

A correção era adicionar AD_BREAK_SKIPPED se um anúncio fosse ignorado.

* Zendesk #4496 - Stream Integrity: Erro 102100 com redirecionamentos para fluxos token.

A correção foi adicionar suporte para a configuração da propriedade AVNetworkConfiguration useCookieHeaderForAllRequests por meio do TVSDK.

* Zendesk #17179 - Reprodutor de Flashes travando em várias alterações SAP para conteúdo criptografado.

Corrigida uma falha durante a reprodução de algum conteúdo criptografado.

**Observação**: A correção exige o Flash Player 19.0.0.200 ou superior.

* Zendesk #17499 - como não remover os midrolls após o relógio, mas remover a pré-rolagem do conteúdo de transferência

Adicionado um tipo a AdBreakTimelineItem (AdBreakTimelineItem.placementType) para que AdPolicySelector possa retornar uma política diferente para conteúdo precedente, intermediário e posterior à rolagem.

* Zendesk #17665 - Limitação da largura de banda

A correção era remover a lógica para alterar o tamanho do buffer do público alvo para o tamanho inicial do buffer quando o buffering começava.

**Versão 1.14.14** (1.4.14.771)

* Zendesk #17363 - Corrigir a documentação README para o player de referência

   * Instruções para baixar e instalar o playerglobal.swc.
   * Adicione instruções para atualizar a configuração do projeto com uma versão específica do Flash Player.
   * Atualize a configuração do projeto AdvertisingOverlay para usar a versão mínima do player.
   * Atualize a configuração do projeto do ReferenceCore para usar a versão 11.9 do player específico

* Zendesk #17471 - Congelamentos do player

Correção parcial para um problema em que um anúncio não é reproduzido do início após a busca.

* Zendesk #17496 - Podbuster não é resolvido ao buscar novamente na janela do DVR

Forneça parâmetros personalizados para cada intervalo de anúncios.

**Versão 1.4.13** (1.4.13.660)

* Zendesk #4037 - No Useable Perfil Error (requer o Flash Player 18.0.0.232 ou superior)

corrigir problema de análise de url quando o parâmetro do query contém &quot;http&quot;

* Zendesk #4260 - Flash Player 18 falha no IE11 (requer Flash Player 18.0.0.232 ou superior)

Corrigida uma falha ao reproduzir vídeo no modo de tela cheia com IE11

* Zendesk #4262 - Adobe Primetime player trava no Windows 10 (requer Flash Player 18.0.0.232 ou superior)

Corrigida uma falha ao reproduzir vídeo no modo de tela cheia com o FireFox no Windows.

* Zendesk #4279 - HLS TVSDK ad insert -302 problema de redirecionamento no iOS e na área de trabalho

Correção de um problema em que um URL não era reconhecido corretamente porque não tinha extensão

* Zendesk #4306 - Falha de Flash Player ao acessar tela cheia somente no Win (requer Flash Player 18.0.0.232 ou superior)

Corrigida uma falha ao reproduzir vídeo no modo de tela cheia no Windows.

* Zendesk #4480 - eventos de tag ID3 ausentes (requer o Flash Player 18.0.0.232 ou superior)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI e CRS | Reforço: Tratar elementos dinâmicos em determinados URLs de arquivos de mídia.

Serviço de reempacotamento da Creative para lidar corretamente com anúncios com URLs criativos dinâmicos.

* PTPLAY - 2114 - Suporte para reprodução MP4.

A reprodução básica de conteúdo MP4 agora é compatível, incluindo reprodução, pausa e busca.

As seguintes opções exigem o Flash Player 18.0.0.225 ou superior:

* Zendesk #3992 - Velocidades adicionais do TrickPlay.

O TrickPlay agora aceita taxas superiores a 16x: +/-32, +/-64 e +/-128.

* Zendesk #3113 - Falha no plug-in do Flash Player

Corrigida uma falha ao tentar reproduzir um anúncio de redirecionamento no Mac Firefox.

* Zendesk #4037 - No Useable Perfil Error (Erro no zero ao usar o zero)
* Zendesk #4262 - Adobe Primetime player trava no Windows 10

Corrigida uma falha no Windows Firefox durante a reprodução em tela cheia.

**Versão 1.4.11** (1.4.11.648)

* Zendesk #1869 - Issue Changing Font Size (edição que altera o tamanho da fonte) (requer o Flash Player 18.0.0.200)

Permitir que tamanhos de legenda sejam usados no código de legenda WebVTT.

* Zendesk #3113 - Flash Player Plugin Crashes (requer o Flash Player 18.0.0.200)
* Zendesk #3268 - Desktop: Start do player de vídeo oscilando após +- 40/50 segundos e start ficando pretos após +- 90 segundos (requer o Flash Player 18.0.0.200)

Corrigir erro de vídeo de estágio.

* Zendesk #3670 - Erro INVALID_PARAMETER no VOD ao buscar no Reprodutor de referência (requer o Flash Player 18.0.0.200)

InvalidateProfiles em ThreadSeek quando um novo período é detectado.

* Zendesk #3896 - Flash Player crash with Stream Integrity set to ON on Chrome (requer Flash Player 18.0.0.200)

Corrigida uma falha no modo de rede nativo no pimenta

* Zendesk #3905 - O player TVSDK não é carregado quando hospedado no CDN

Correção de problemas ao localizar o token curinga quando pageDomain é diferente do domínio swf.

**Versão 1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player trava Flash no Firefox

Corrigida uma falha ocasional de Flash Player com o Firefox no Mac quando um fluxo, reproduzido em um monitor externo, alternava para um fluxo de taxa de bits mais alta.(requer o Flash Player 18.0.0.160)

* Zendesk #3268 - Desktop: Start do player de vídeo oscilando após `+-` 40/50 segundos e start ficando pretos após `+-` 90 segundos

Correção de um problema no Mac Chrome em que o fluxo era start para oscilar e eventualmente ficar preto. (requer o Flash Player 18.0.0.161)

* Zendesk #3304 - macro VAST 3.0 `[ERRORCODE]` não sendo preenchida

   * o código de erro 400 será exposto se o anúncio em linha apresentar anúncios mal criados.
   * `[ERRORCODE]` macro será codificada em URL

* Zendesk #3601 - Solicitação de aprimoramento: Gerenciamento do companheiro de invólucro

   * O TVSDK exibirá o companheiro de wrappers que contém recursos (html, iframe ou estáticos) próximos ao embutido. (se a linha em linha não contiver uma para esse tamanho)
   * Os contêineres associados com recursos, a menos que sejam usados para exibição, serão ignorados. (não usar para rastreamento )
   * Somente companheiros de invólucro com o recurso NO serão usados para fins de rastreamento. (companheiro de invólucro que contém apenas rastreamento )

**Versão 1.4.9**

* Zendesk #2615 - problema ao remover a visualização HLS da tela do desktop

Método clearVideo() adicionado ao MediaPlayer. Limpa o quadro de vídeo exibido apagando o AVStream do objeto StageVideo. Só deve ser chamado se o vídeo estiver pausado e replaceCurrentResource ou replaceCurrentItem deve ser chamado antes que play() possa ser chamado novamente.

* Zendesk #3169 - Atualização do player de referência com integração Adobe Analytics

O player de referência foi atualizado com a integração do Adobe Analytics

* Zendesk #3296 - Desktop HLS TVSDK - Anúncios de terceiros VAST que não são reproduzidos

os tipos mime para o formato HLS faziam distinção entre maiúsculas e minúsculas, isso estava incorreto e foi alterado, portanto, não fazem mais distinção entre maiúsculas e minúsculas

**Versão 1.4.8**

* Zendesk #2737 - Desktop Player - Erro 106000 (requer o Flash Player 17.0.0.184)
* Zendesk #3007 - Anúncios precedentes que não aparecem após a atualização para o Flash Player 17 (requer o Flash Player 17.0.0.184)
* Zendesk #3085 - Desktop HLS Player Thlines 106000 Erro após 60 segundos (requer o Flash Player 17.0.0.184)

**Versão 1.4.7**

* Zendesk #2760 - Tag DISCONTINUITY ignorada durante o modo TrickPlay (requer a versão 17.0.0.158 do Flash Player)
* Zendesk #2760 - Tag DISCONTINUITY ignorada durante o modo TrickPlay (requer a versão 17.0.0.158 do Flash Player)

**Versão 1.4.6**

* Zendesk #2652 - Documentação do Auditude para HLS de desktop, Clarified Auditude media_id para documentação HLS de desktop

**Versão 1.4.5**

* Zendesk #2256 - Acesso à Playlist Principal, PSDK atualizado para despachar eventos timedMetadata para marcas assinadas na lista de reprodução principal. (requer a versão 17.0.0.134 do Flash Player)
* Zendesk #2417 - Player trying to download legendas before playback start, WebVTT estava usando a variável de número de segmento errada para a correspondência de número de segmento. Erros só apareciam para mídias que tinham índices de segmentos começando em zero. (requer a versão 17.0.0.134 do Flash Player)
* Zendesk #2537 - O player do Flash trava ao usar o plug-in de pimenta com o Chrome (requer a versão 17.0.0.134 do Flash Player)
* Zendesk #2547 - Legendas árabes: O texto deve ser alinhado justificado à direita (requer a versão 17.0.0.134 do Flash Player)

**Versão 1.4.4**

* Zendesk nº 1561 - Re: `[Adobe Primetime]` Atualização: Suporte a failover baseado em cliente HLS para PROGRAMA-DATE-TIME no PSDK de desktop (requer a versão 16.0.0.305 ou superior do Flash Player)
* Zendesk #2197 - Rastreamento de erros de anúncio `[Ads]`
* Zendesk #2286 - Solicitação de recurso: Forneça informações sobre o status de carregamento do anúncio (VPAID)
* Zendesk #2285 - Solicitação de recurso: Ignorar anúncio após uma duração de tempo limite especificada
* Erro #3921755 - Atualização da biblioteca OpenSSL para a versão 1.0.1L no Flash Player (requer a versão 16.0.0.305 do Flash Player ou superior)

**Versão 1.4.2**

* Zendesk #1303 - Deslocamento vertical para legenda fechada (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento esperada: dezembro de 2014)
* Zendesk #1870 - Closed Caption On &amp; Off (Legenda fechada ativada e desativada) (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento esperada: dezembro de 2014)
* Zendesk #2110 - A reprodução trava depois de tentar entrar na tela cheia durante um anúncio VPAID (requer a versão 16.0.0.235 do Flash Player ou superior, data de lançamento esperada: dezembro de 2014)
* Zendesk #2199 - `[VPAID]` Player not responding when search previous ad break
* Zendesk #2358 - Re: `[Analytics]` Dados de capítulo incorretos

**Versão 1.4.1**

* Atualização da API de blecautes para ser consistente com a implementação do Android e do iOS.

**Versão 1.4.0**

* Zendesk #1024 - Recurso para remover anúncio do fluxo via manifesto
* Zendesk #1423 - A falha de reprodução HLS está travando o Flash Player (sem relatório de erro)
* Zendesk #1674 - ClosedCaption Not appear up, correct 708 caption display when 0x03 ETX codes is missing. (Zendesk #1674 - ClosedLegtion Não exibido, exibição correta da legenda 708 quando os códigos ETX 0x03 estiverem faltando.

## Problemas conhecidos {#known-issues}

* A Legenda fechada não funcionará com conteúdo somente de áudio porque o sistema de legenda precisa de vídeo para funcionar.
Sem vídeo, não há dimensão viewport e, sem uma dimensão viewport, não é possível exibir gráficos para legendas.
* A integridade do fluxo é um pouco mais lenta no Google Chrome devido às restrições da caixa de proteção do Chrome.
* No TVSDK 1.4, se você desativar o autoPlay, um erro de DRM pode ocorrer quando o player permanece inativo por pelo menos um minuto. Para contornar esse problema, ao desativar a reprodução automática, mas pré-carregar ativos, modifique `ReferenceCore.as` alterando o conteúdo de `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versão 1.4.13** PTPLAY-8501 - Quando o VMAP retorna dois anúncios MP4 diretos não transcodificados, o mesmo fallback é reproduzido duas vezes.

* **Versão 1.4.2** Na versão 16 do Flash Player, um problema foi identificado com a lógica de &quot;desativação&quot; do ABR, depois que o player entra em um evento de buffering vazio. O problema impede que a taxa de bits diminua em ambientes de largura de banda defeituosos quando o player entra em um estado de buffering. Para contornar o problema, faça com que seu aplicativo defina `BufferControlParameters.initialBufferTime` o como sendo `BufferControlParameters.playbackBufferTime` temporariamente durante o estado de buffering (ou seja, em um `BufferEvent.BUFFERING_BEGIN` evento) e redefina-o para os valores definidos no `BufferEvent.BUFFERING_END` evento. A correção para esse problema estará disponível na próxima versão de patch da versão 16 do Flash Player.

* **Versão 1.4.0**

   * PTPLAY-1634 - A mesma tag Assinada tem carimbos de data e hora diferentes em janelas ativas diferentes. Quando as janelas ativas se movem, a mesma tag em cada uma delas deve ter os mesmos carimbos de data e hora. No entanto, às vezes, as mesmas tags têm carimbos de data e hora diferentes.
   * PTPLAY-28 - A linha do tempo do MediaPlayer não inclui quebras vazias.
   * Um arquivo de política entre domínios (crossdomain.xml) é necessário para permitir a transmissão de conteúdo de um domínio diferente. [Configuração de um arquivo crossdomain.xml para streaming](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)HTTP.
   * Bug #3694203 - Em um fluxo DVR, procurar dentro de um mid-roll em outra dica de anúncio intermediário pode levar ao congelamento do navegador
   * Bug #3753725 - selectPolicyForSeekIntoAd não leva em conta se o intervalo do anúncio foi observado
   * Erro #3754529 - Os anúncios anteriores não são removidos do fluxo ao buscar novamente em um fluxo DVR ao vivo
   * Erro #3761896 - Se a busca for permitida durante a reprodução do anúncio, os marcadores do anúncio serão reajustados após a busca. A solução alternativa é não usar o retorno de chamada ITEM_UPDATED durante a busca
   * Bug #3779889 - A chamada completa não é feita ao chegar ao fim na reprodução de truques no Video Analytics
   * Erro #VA-779 - A pulsação de evento de alteração de taxa de bits não é enviada para Análise de vídeo aprimorada com implementação de referência de suporte de pulsação - A reprodução de truque não é implementada no aplicativo de amostra.

## Recursos úteis {#helpful-resources}

* Consulte a documentação completa da ajuda na página Aprendizagem e suporte [da](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
