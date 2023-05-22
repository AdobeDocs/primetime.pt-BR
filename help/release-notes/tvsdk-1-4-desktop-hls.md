---
title: Notas de versão do TVSDK 1.4 para HLS para desktop
description: As Notas de versão do TVSDK para HLS para desktop descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 5e227c99-acf6-4b16-a35a-68e2928fdbfd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '5195'
ht-degree: 0%

---

# Notas de versão do TVSDK 1.4 para HLS para desktop {#tvsdk-for-desktop-hls-release-notes}

As Notas de versão do TVSDK para HLS para desktop descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no TVSDK DHLS.

## Novos recursos {#new-features}

**1.4.31**

* **Suporte a várias CDNs para anúncios CRS**

   * Por padrão, todos os ativos transcodificados serão hospedados no CDN de propriedade do Adobe no Akamai. Com a versão mais recente, o Adobe Creative Repackaging Service (CRS) fornece a capacidade de fazer upload dos dispositivos de criação transcodificados para vários CDNs, conforme especificado pelo cliente.
   * Novas APIs são adicionadas ao TVSDK para permitir a especificação do URL criativo final do CRS quando o URL padrão não for usado. Consulte a documentação para saber como usar essas novas APIs.

### Novos recursos nas versões anteriores {#new-features-previous}

**1.4.30**

* **Métricas de cobrança**

Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.

**1.4.24**

* **Conexão de rede persistente**

Adobe Importante: você deve ter pelo menos o Flash Player versão 22 ou posterior instalado.
As conexões de rede persistentes criam e armazenam uma lista interna de conexões de rede que podem ser reutilizadas para várias solicitações, em vez de abrir uma nova conexão para cada solicitação de rede. As conexões de rede persistentes devem aumentar a eficiência e diminuir a latência no código de rede.

Nesta versão, esse recurso não é compatível com o Apple Safari e o Mozilla Firefox em uma Mac.

**1.4.19**

* Suporte à integridade do fluxo para anúncios VPAID.
* Ativada a opção de guia Mudo no Flash player FP 20.0.0.267 para Firefox 42 e posterior, corrigindo o problema de travamento.

**1.4.18**

* O TVSDK HLS para desktop do Primetime agora é compatível com criações de SWF linear VPAID 2.0 para habilitar uma experiência avançada de anúncios interativos em fluxo.

**1.4.10**

* **Fallback de anúncios, encadeamento de Daisy na lógica de seleção de anúncios (Zendesk #3103)** Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Fallback de anúncios para anúncios VAST e VMAP](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Biblioteca de Video Heartbeats (VHL) atualizada para a versão 1.5**

   * Capacidade de enviar metadados com início de vídeo e/ou início de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - As pulsações são menores em média e menores em tamanho.

**1.4.7**

* **Suporte à individualização no local**

Suporte para instalações locais do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para ir para um endpoint diferente.

**1.4.6**

* **Exemplo de criptografia AES (requer o Flash Player versão 17.0.0.134)**

A criptografia AES baseada em amostra agora é compatível.

**1.4.2**

* **Atualização da Biblioteca de vídeo Heartbeats (VHL) para a versão 1.4.0.1**

   * Adição da capacidade de reunir diferentes casos de uso de análise, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete. O ad break é inferido das chamadas de método trackAdStart e trackAdComplete.
   * A propriedade de indicador de reprodução não é mais necessária ao rastrear anúncios.

**1.4.0**

* **Sinalização De Blecaute Com Substituição De Conteúdo Alternativo** Como parte da atualização do TVSDK 1.4, o TVSDK também oferece suporte à entrada e ao retorno de blecautes regionais em relação ao conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando a programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remova/substitua anúncios C3** Agora, nenhum trabalho preparatório adicional é necessário para inserir dinamicamente novos anúncios nos ativos de vídeo sob demanda (VOD) que saem da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova e poderosa funcionalidade também é útil nos casos em que o conteúdo ao vivo/linear é transmitido e é imediatamente desativado para uso como conteúdo sob demanda sem o tempo adequado para &quot;limpar&quot; o ativo.

## Problemas resolvidos {#resolved-issues}

>[!NOTE]
>
>Todos os clientes de TVSDK que usam CRS são altamente incentivados a atualizar para pelo menos TVSDK 1.4.32 no iOS, Android e Desktop HLS. Essa atualização será uma substituição da implementação do aplicativo existente. Após a atualização, verifique as solicitações do URL criativo do CRS em uma ferramenta de proxy (por exemplo, Charles) para verificar se a versão no caminho reflete a versão 3.1. Por exemplo,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versão 1.4.41**

* Zendesk #33777 - SWF de token localhost para build de distribuição DHLS expirado.

   Atualização do token localhost para demonstração PMP no DHLS.

### Problemas resolvidos nas versões anteriores {#resolved-issues-previous}

**Versão 1.4.38** (891)

* Zendesk #30731 - O TVSDK não reproduz vários anúncios VPAID em um AdBreak.

   Correção da reprodução de vários anúncios VPAID em um AdBreak.

* Zendesk #29968 - Billboard Dupla.

   O reprodutor de vídeo pode repetir o último segmento de um período em que ocorre um switch ABR. Devido a isso, às vezes, o último segmento da pré-rolagem se repetiu. Isso foi corrigido.

**Versão 1.4.35** (879)

* Zendesk #26058 - Suporta eventos VPAID nativos

**Versão 1.4.33** (873)

* Zendesk #21701 - Envie o URL criativo original para a solicitação 1401 CRS em vez do URL normalizado.

   O problema em que URLs já reempacotados estão sendo solicitados para transcodificação foi corrigido, de acordo com o exigido pelo back-end do CRS.
* Zendesk #26197 - Compactação anamórfica não repetida na Resolução de Exibição desejada.

   **Nota**: esse problema exige o Flash player 24.0.0.194 ou posterior.

   O problema em que as entradas ausentes nas tabelas de proporção eram usadas para calcular a largura da saída foi corrigido.

* Zendesk #26840 - Falha na detecção de HDCP no IE11 + Windows7 após a segunda tentativa.

   **Nota**: esse problema exige o Flash player 24.0.0.218 ou posterior.

   Esse problema foi resolvido modificando o processamento da fila de mensagens principal do AdobeCP para iterar por toda a fila, em vez de apenas bloquear na primeira mensagem.

* Zendesk #27460 - A nova conta Akamai não pode lidar com uma solicitação CDN POST.

   A nova conta CDN não pode lidar com uma solicitação CDN POST. Esse problema foi resolvido atualizando o código para fazer com que a solicitação de anúncio cdn.auditude.com fosse GET em vez de POST.
* Zendesk #27619 - Flash crash no Windows 10

   **Nota**: esse problema exige o Flash player 24.0.0.218 ou posterior.

   Esse problema era resolvido evitando uma falha como resultado de URLs longos.

* Zendesk #28218 - O evento de rastreamento não é acionado enquanto o reprodução do ponto de retomada

   Esta edição é a mesma edição do Zendesk #26592. O problema em que as operações de busca eram permitidas quando o reprodutor de mídia estava no estado PREPARADO para fluxos de VOD foi corrigido.

**Versão 1.4.32** (867)

* O evento de rastreamento do Zendesk #26592 não é acionado quando a reprodução começa a partir do ponto de retomada

O código não estava atualizando o item de ad break precedente quando o ponto de retomada não era zero. Esse problema foi resolvido adicionando lógica para atualizar o código quando os horários de início do intervalo não correspondem.

* Os anúncios do Zendesk #27022 não estão sendo reproduzidos na segunda vez que um ativo é reproduzido

As exceções com os métodos de matriz foram corrigidas.

**Versão 1.4.30** (855)

Os seguintes problemas foram resolvidos para TVSDK nesta versão:

* Zendesk #22898 - A falta de legendas não deve causar falha na reprodução.

**Nota**: esse problema exige o Flash player 23.0.0.185 ou posterior.

Esse problema foi resolvido permitindo que o TVSDK continuasse a reprodução, mesmo se o manifesto não tiver o WebVTT M3U8, e apenas registrando um aviso.

* Zendesk #23454 - Anúncios de terceiros (VPAID) não são tratados corretamente

Esse problema era resolvido ao manipular corretamente os anúncios VPAID com base em IDs de conteúdo em vez de intervalos de tempo.

* Zendesk #24528 - Métricas de uso do TVSDK para faturamento.

Importante: esse problema exige o Flash player 23.0.0.185 ou posterior.

* Zendesk # 25432 Problema de legendas ocultas durante o redimensionamento do player.

Importante: esse problema exige o Flash player 23.0.0.185 ou posterior.

O código do mapa de textura de exibição da legenda foi corrigido para lidar corretamente com as coordenadas durante o redimensionamento do player.

A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

* Zendesk #23730 - As métricas da taxa de bits estão em branco

Esse problema foi resolvido com o rastreamento das alterações na taxa de bits no VideoAnalyticsTracker.

* Adição de uma nova API, assetDuration, a PTVideoAnalyticsTrackingMetadata para atualizar a duração do ativo para fluxos Live/Linear.

**Versão 1.4.28** (848)

* Zendesk #25027 - O Auditude não funciona na versão 1.4.27 para desktop

Esse problema foi resolvido adicionando o código para verificar a AUDITUDE_METADATA_KEY e tornando as AUDITUDE_METADATA_KEY e ADVERTISING_METADATA_KEY intercambiáveis.

* Zendesk #24428 - Problema frequente de buffering usando o TVSDK para reproduzir um DRM HLS

Esse problema foi resolvido levando em conta que, quando não há configuração de anúncio, o TVSDK pode acelerar o processamento eliminando a suspensão de anúncio antes da exibição e a suspensão de reserva em tempo real na linha do tempo projetada para sincronizar a inserção de anúncios.

* Zendesk #24344 - Desativar arquivos WebVTT para melhorar os tempos de inicialização.

**Nota**: esse problema exige o Flash player 23 ou posterior.

Esse problema foi resolvido carregando os arquivos WebVTT somente quando é necessário exibir as legendas.

* Zendesk #24994 - As legendas ocultas são retiradas do jogador ao voltar do intervalo comercial

**Nota**: esse problema exige o Flash player 23 ou posterior.

O código EOC artificial fez com que a exibição da legenda desaparecesse. Esse problema foi resolvido forçando os códigos de legenda 608 RU2, RU3 e RU4 a fornecerem a visibilidade correta na janela ativa atual.

**Versão 1.4.27** (844)

* Zendesk #21554 - beacons de erro do TVSDK não acionados para o tipo de aplicativo = video/mp4

Esse problema foi resolvido habilitando o TVSDK para executar ping nos URLs de rastreamento de erros corretos em formatos de ativos inválidos.

* Zendesk #23402 - Reprodução de anúncios incompleta

**Nota**: esse problema exige o Flash player 23 ou posterior.

Depois de receber um erro 404 em determinadas solicitações, pode ocorrer uma falha. Esse problema foi resolvido garantindo que a conexão não seja desligada enquanto a resposta estiver sendo tratada. A resolução garante que os arquivos de anúncios VPAID não sejam contados incorretamente para que não sejam liberados durante o download.

* Zendesk #23621 - A tentativa está falhando nos 400 e 404

**Nota**: esse problema exige o Flash player 23 ou posterior.

Correção do problema que causava a corrupção de metadados de DRM ao alternar entre perfis diferentes.

* Zendesk #23705 - Congelamento de anúncios de vídeo durante interrupções de AdStitched

**Nota**: esse problema exige o Flash player 23 ou posterior.

Esta edição é a mesma edição do Zendesk #23621.

* Zendesk #23905 - Alguns ad breaks ignoram ad breaks

**Nota**: esse problema exige o Flash player 23 ou posterior.

O código de rede nativo do Windows foi corrigido para garantir que as conexões não fechem identificadores que estão sendo usados no momento por outras conexões.

* Ticket #24029 - Os fluxos FER da HLS não reproduzem todos os anúncios intermediários no arquivo .json intermediário.

Esse problema foi resolvido permitindo que os clientes definissem parâmetros personalizados separadamente na instância da Oportunidade para que os clientes não precisassem substituir o OpportunityGenerator.

**Versão 1.4.26** (839)

* Zendesk #18854 - Atualizar a lógica de seleção criativa com base nas regras CRS
   * Forneceu suporte para atualizar a lógica de seleção criativa com base nas regras de CRS

* Zendesk #22725 - implementação de playbackManager.beginPlayback() no aplicativo de amostra para desktop

   * Correção ao remover essa chamada redundante no final de startPlaybackFromFlashVars conforme o método é chamado de setupVideo()

* Zendesk #22807 - Exceção de referência nula do SeekManager

   * Correção ao fornecer a proteção necessária de ponteiro NULL no SeekManager relacionada ao _dispatcher

* Zendesk #22822 - Buffering frequente ao usar o TVSDK para reproduzir um HLS claro

   * Corrigido removendo a oportunidade inicial gerada por adSignalingModeOpportunityGenerator se não houver nenhum anúncio

* Zendesk #23378 - Blocos de integridade de fluxo rules.xml

   * Correção ao carregar o arquivo rules.xml por meio do workflow de integridade do fluxo de trabalho

**Versão 1.4.24** (817)

* Zendesk #19851 - Quando o player se adapta a uma taxa de bits diferente, ele salta alguns quadros no tempo na nova taxa de bits, tornando uma experiência estranha

**Nota**: esse problema exige o Flash player 22.0.0.175 ou posterior.

O problema em que o adaptador DRM é redefinido após o download de uma pequena fração de um segmento que não é restaurado corretamente foi resolvido.

* Zendesk #20784 - Analytics: Conclusões de acionamento de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido adicionando uma API (trackVideoComplete) para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo LINEAR/LIVE.

As seguintes bibliotecas foram atualizadas:

* Zendesk #21643 - Anúncios VPAID não são reproduzidos na íntegra

   * Biblioteca do AdobeMobile para 4.10.0
   * Biblioteca do VHL para 1.5.6
   * Biblioteca VHL-Nielsen para 1.6.7

Esse problema era resolvido usando uma janela de visualização de altura zero para preencher o estágio quando um anúncio VPAID era reproduzido.

* Zendesk #22110 - Analytics: Adicionar um h:sc:campo ssl para as chamadas de rastreamento de heartbeat

Os problemas relacionados ao SSL foram corrigidos e a biblioteca do VHL usada no TVSDK foi atualizada para a versão mais recente.

* Zendesk #22608 - Vídeo mostra intermitentemente uma tela preta (requer o Flash Player 22.0.0.175 ou posterior)

Durante a taxa de bits adaptável, com o limite máximo de taxa de bits, o recarregamento do vídeo mostra intermitentemente uma tela preta, mesmo que o cliente veja as atualizações para a posição e se comporte como se estivesse reproduzindo o conteúdo.

**Versão 1.4.23** (809)

* Zendesk #2887 - problema de cancelamento de anúncios após a exibição quando a lógica da Regra de anúncio era aplicada ao TVSDK

**Nota**: esse problema exige o Flash player 21.0.0.240 ou posterior.

O problema em que os anúncios posteriores à exibição eram ignorados quando a lógica da regra de anúncio era aplicada ao TVSDK foi corrigido.

* Zendesk #19863 - Anúncio com arquivo de mídia VPAID descartado

Se um anúncio em linha vasto tiver vários arquivos de mídia com um anúncio VPAID sendo o primeiro anúncio, o anúncio em linha não será reproduzido para fluxos ao vivo. Esse problema foi resolvido selecionando um arquivo de mídia diferente.

* Zendesk #21021 - Áudio de ligação tardia que causa repetições de segmento de áudio

**Nota**: esse problema exige o Flash player 21.0.0.240 ou posterior.

O problema de repetição de áudio foi corrigido.

* Zendesk #21125 - Retorno de ad break ao vivo/linear com antecedência

**Nota**: esse problema exige o Flash player 21.0.0.240 ou posterior.

Esta versão oferece suporte para retornar de um ad break antecipadamente antes que o ad break seja reproduzido até a conclusão. O retorno antecipado é indicado por meio de uma tag de manifesto personalizada.

* Zendesk # 21369 Áudio de ligação tardia causa um tempo inconsistente

**Nota**: esse problema exige o Flash player 21.0.0.240 ou posterior.

O problema de repetição de áudio que foi corrigido também corrigiu esse problema.

* Zendesk #21760, 20921 - Dessincronização de áudio e vídeo na busca.

**Nota**: esse problema exige o Flash player 21.0.0.240 ou posterior.

O problema de repetição de áudio foi corrigido.

* Zendesk #22024 - Erro ao executar o TVSDK

O problema em que o reprodutor de referência não reproduzia nenhum fluxo e gerava uma exceção na inicialização foi corrigido.

**Versão 1.4.22** (791)

* Zendesk #17580 - Erro de tempo de execução do Primetime com o código 3357

**Nota**: esse problema exige o Flash player 21.0.0.197 ou posterior.

Os erros aleatórios 3357 que ocorreram ao inicializar corretamente deviceID quando storeVoucher() é chamado foram corrigidos.

* Zendesk #21334 - Valor de tempo limite de solicitação de anúncio TVSDK para solicitações de anúncios de terceiros

Nesta versão, o tempo limite global da solicitação de anúncio foi adicionado.

**Versão 1.4.21** (782)

* Zendesk #19580 TVSDK aguarda a conclusão do resolvedor de conteúdo antes de enviar `PTTimedMetadataChangedNotification` notificações

**Nota**: esse problema exige o Flash player 21.0.0.182 ou posterior.

Esse problema foi resolvido no reprodutor de referência de desktop fornecendo a capacidade de definir tags de anúncio e adicionar um gerador de oportunidades personalizado que mostra como assinar dicas personalizadas e como processá-las em um arquivo VOD.

* Zendesk #20806 Futuros anúncios intermediários na janela DVR não serão acionados após Trocar câmeras

**Nota**: esse problema exige o Flash player 21.0.0.182 ou posterior.

Esse problema foi resolvido atualizando o aplicativo para definir _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) para desativar a inserção de anúncio antes da exibição em uma troca PIP e, como resultado, nenhuma oportunidade antes da exibição é gerada.

Uma funcionalidade de classificação foi introduzida para corrigir o posicionamento de anúncios fora de sequência que resultou em uma duração negativa do conteúdo principal.

* Zendesk #20522: Não é possível ignorar anúncios VPAID 2.0

**Nota**: esse problema exige o Flash player 21.0.0.182 ou posterior.

* Esse problema foi resolvido ignorando os anúncios VPAID durante o perdão de anúncios.
* Quando a política adbreak está definida como ignorar, os eventos ad break e ad break ainda são despachados. O estado do player é inconsistente.

Esse problema foi resolvido para se comportar corretamente e não despachar eventos quando o ad break é ignorado.

* Zendesk #20955 Definir pares de valores-chave na propriedade customParameters por meio do gerador de oportunidades

**Nota**: esse problema exige o Flash player 21.0.0.182 ou posterior.

A Solicitação de Auditoria analisa as Configurações de Auditoria em busca de parâmetros personalizados ao criar uma unidade de publicidade para solicitações de publicidade.

Esse comportamento foi alterado para incluir parâmetros personalizados do objeto Oportunidade na solicitação. Além disso, várias oportunidades com parâmetros personalizados diferentes não podem ser compactadas em uma solicitação do Auditude.

* Zendesk #21227 - m3u8 não jogam de forma consistente

**Nota**: esse problema exige o Flash player 21.0.0.211 ou posterior.

Esse problema foi resolvido permitindo que o TVSDK ignorasse o manifesto (subperfis HLS) que contém o codec AC3 para o qual o TVSDK não oferece suporte (surround).

**Versão 1.4.20** (762)

* Zendesk #19181 - Truque jogar rápido para frente para ponto ao vivo bloqueia fluxo.

**Nota**: esse problema exige o Flash player 20.0.0.306 ou posterior.

* Zendesk #19286 - Ocorreu uma falha no Flash Player ao buscar de um lado para o outro em um fluxo de FER.

**Nota**: esse problema exige o Flash player 20.0.0.306 ou posterior.

As interrupções ocasionais que ocorreram ao buscar no Google Chrome foram resolvidas ao desligar as consultas, se as consultas demorarem muito para obter uma resposta ou se o soquete estiver sendo desligado.

* Zendesk #19305 - Reprodução instável encontrada ao reproduzir um fluxo com descontinuidades A/V.

**Nota**: esse problema exige o Flash player 20.0.0.306 ou posterior.

Esse problema foi resolvido informando um aviso.

* Zendesk # 19359 - Flash Player falhou devido à posição do atributo #EXT-X-FAXS-CM: no manifesto de nível de conjunto.

Esse problema foi resolvido quando a tag #EXT-X-FAXS-CM aparece na lista de reprodução principal antes da taxa de bits individual ou dos segmentos na lista de reprodução.

* Zendesk #19489 - Fast Forward para o Live Point paralisa plug-in (transmissão ao vivo)

Esta edição é a mesma do Zendesk #19181.

* Zendesk #19699 - TVSDK falha ao alternar entre faixas de legendas WebVTT

Esse problema era resolvido fazendo o despejo do reprodutor e recarregando o manifesto quando um rastreamento era alterado e corrigindo o problema de conversão de sequência de caracteres UTF8 que afetava os nomes de rastreamento da legenda WebVTT de dois bytes.

**Versão 1.4.19** (1.4.19.738)

* Zendesk #18234 - Flash Player trava reproduzindo os fluxos com strings Unicode em CC

Esse problema exige o Flash Player FP 20.0.0.267 ou posterior e foi resolvido manipulando a cadeia de caracteres Unicode corretamente.

* Zendesk #18304 - Suporte à Integridade de Stream para Anúncios VPAID

Esse recurso exige o Flash Player FP 20.0.0.267 ou posterior e foi introduzido na versão 1.4.19.

* Zendesk #18766 - O Reprodutor de Referência é incapaz de exibir caracteres unicode não latinos nos nomes de faixas do CC

Esse recurso exige o Flash Player FP 20.0.0.267 ou posterior e foi corrigido ao manipular corretamente a cadeia de caracteres Unicode.

* Zendesk #18804 - Jogador trava no Firefox 42

Este problema requer o Flash Player FP 20.0.0.235 ou posterior e é o mesmo problema que o Zendesk #18723.

* Zendesk #18864 - falha total do plug-in do Flash Player

Esse problema exige o Flash Player FP 20.0.0.235 ou superior e é o mesmo que Zendesk #18723.

* Zendesk #18998 - Se os carimbos de data e hora de áudio e vídeo não corresponderem, ocorreu um download infinito de segmentos em descontinuidade.

Esse problema foi resolvido ignorando a lacuna entre os carimbos de data e hora e apenas reproduzindo o conteúdo baixado.

* Zendesk #19093 - Anúncios intermediários só podem ser assistidos uma vez com conteúdo ao vivo e reprodução de evento completo (FER), mas esses anúncios não puderam ser assistidos novamente quando o encaminhamento rápido ou a busca ultrapassam os anúncios

No seletor adPolicy padrão do Primetime, se um anúncio intermediário for assistido, o adBreak não será movido para a posição buscada quando você concluir uma busca. Para reproduzir o anúncio novamente, após a busca, o aplicativo precisa substituir a função selectAdBreaksToPlay().

* Zendesk #19101 - Retroceder anúncios não resolvidos do Midroll remove a inserção do anúncio.

Esse problema foi resolvido permitindo que o reprodutor atualizasse o tempo de playbackMetrics, o minimumOpportunityTime e a Linha do tempo.

* Zendesk #19102 - Problemas com o FER e o modo truque

Esse problema requer o Flash Player FP 20.0.0.267 ou posterior e foi resolvido definindo-se corretamente advertisingMetadata.adSignalingMode.

* Zendesk #19175 - Às vezes, os anúncios antes da exibição não são exibidos na primeira vez que o fluxo é reproduzido.

Esse problema foi resolvido adicionando uma nova API, adRequestTimeout, às AuditudeSettings para um tempo limite de solicitação de anúncio. Agora, os usuários podem substituir o tempo limite padrão de solicitações de anúncios 10s.

**Versão 1.4.18** (1.4.18.722)

* Zendesk #3324 - Os relatórios de anúncios do Primetime não rastreiam ad breaks quando não há mídia de anúncio em um VMAP.

Quando um ad break está vazio, o início do ad break e os eventos de rastreamento de conclusão não eram tocados. Esse problema era resolvido enviando pings de início de ad break em ad breaks vazios, como VMAP AdBreak, com um nó AdSource válido.

**Versão 1.4.17** (1.4.17.702)

* Zendesk #17168 - As legendas não aparecem por cerca de 10 segundos após alternar a visibilidade

Esse problema foi resolvido fornecendo suporte para a tag EXT-X-MEDIA-TIME para arquivos de legenda vtt.

* Zendesk #17983 - Falha ao baixar chaves para um manifesto faz com que toda a reprodução do manifesto falhe

**Nota**: você deve ter pelo menos o Flash Player FP 19.0.0.245 ou superior.

Às vezes, ao reproduzir conteúdo ao vivo, pode haver chaves inválidas no manifesto (por exemplo, para períodos de blecaute), mas outros intervalos de tempo podem ter chaves válidas e ainda serão reproduzidos. Anteriormente, quando uma chave que estava listada em um manifesto não podia ser baixada, todo o manifesto falhava. Agora, o manifesto falha somente quando todas as chaves listadas não podem ser baixadas. Se algumas chaves forem válidas, mas não for possível baixar algumas delas, o conteúdo será reproduzido. Ainda falharemos se tentarmos reproduzir um segmento que requer uma chave que não temos.

* Zendesk #18554 - Integridade do Stream que corta os cookies em alguns casos

**Nota**: você deve ter pelo menos o Flash Player FP 19.0.0.245 ou superior.

Correção de um bug no código de manipulação de cookie que poderia truncar valores de cookie.

**Versão 1.4.16** (1.4.16.684)

* Zendesk #3732 - Adicionar suporte para proxies no Chrome para Integridade de Fluxo (requer o Flash Player FP 19.0.0.207 ou superior)

Isso é um aprimoramento.

* Zendesk #4244 - Problemas de transmissão na substituição do PTS

Esse problema foi resolvido detectando a sobreposição e gerenciando a descontinuidade por tipo de carga útil, e não de forma genérica.

* Zendesk #4487 - Rastreamento do canal linear de conteúdo

Esse problema foi resolvido reinicializando o rastreador de heartbeat de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17427 - Integridade do Adobe Stream não funciona por meio de um proxy no Chrome (Win7) ()

**Nota**: a resolução requer o Flash Player FP 19.0.0.207 ou superior.

Esta edição é a mesma do Zendesk #3732.

* Zendesk #17907 - Defasagem no Live Stream do pHLS com o Flash Player 19

**Nota**: a resolução requer o Flash Player FP 19.0.0.207 ou superior.

Esse problema foi resolvido com a manipulação de fluxos ao vivo, em que os domínios dos arquivos TS são alterados ao recarregar o manifesto ao vivo, e os arquivos são baixados duas vezes.

* Zendesk #17931 - conteúdo HLS com tabulação no início falha na reprodução

**Nota**: a resolução requer o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido manipulando fluxos sem áudio nos primeiros 2 segundos do primeiro arquivo TS.

* Zendesk #17934 - Falha na transmissão ao vivo com o Flash 19.0.0.185

**Nota**: a resolução requer o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido ao manipular transmissões em tempo real com o intercalamento de quadros de áudio e vídeo nos limites do segmento.

* Zendesk #17973 - Flash Player mais recente 19.0.0.185 falha durante a metade da exibição

**Nota**: a resolução requer o Flash Player FP 19.0.0.207 ou superior.

O problema foi resolvido com o manuseio de áudio não misto com inserção de anúncio durante a exibição. (A opção do analisador ocorre e, em qualquer ponto da reprodução, o conteúdo é transferido para o anúncio intermediário ou no meio da reprodução do anúncio e assim por diante.)

* Zendesk #18049 - Falha do Flash 19 com o Firefox 42 beta

Esta edição é a mesma do Zendesk #17973.

**Versão 1.4.15** (1.4.15.678)

* Zendesk #4377: Acione o evento AD_BREAK_SKIPPED ao ignorar um ad break por causa da política de anúncios.

A correção foi adicionar AD_BREAK_SKIPPED se um anúncio fosse ignorado.

* Zendesk #4496 - Integridade do fluxo: Erro 102100 com redirecionamentos para fluxos tokenizados.

A correção foi adicionar suporte para definir a propriedade avnetworkConfiguration useCookieHeaderForAllRequests por meio do TVSDK.

* Zendesk #17179 - Flash player falha em várias alterações do SAP para conteúdo criptografado.

Uma falha durante a reprodução de algum conteúdo criptografado foi corrigida.

**Nota**: a correção exige o Flash Player 19.0.0.200 ou superior.

* Zendesk #17499 - como não remover midrolls após assistir, mas remover preroll do conteúdo fer

Adição de um tipo a AdBreakTimelineItem (AdBreakTimelineItem.placementType) para que AdPolicySelector possa retornar uma política diferente para conteúdo antes, durante e depois da exibição.

* Zendesk #17665 - Limitação da largura de banda

A correção foi remover a lógica para alterar o tamanho do buffer de destino para o tamanho do buffer inicial quando o buffering começar.

**Versão 1.14.14** (1.4.14.771)

* Zendesk #17363 - Corrigir a documentação do README para o player de referência

   * Esclareça as instruções para baixar e instalar o playerglobal.swc.
   * Adicione instruções para atualizar a configuração do projeto com a versão específica do flash player.
   * Atualize a configuração do projeto AdvertisingOverlay para usar a versão mínima do player.
   * Atualize a configuração do projeto ReferenceCore para usar a versão 11.9 do player específico

* Zendesk #17471 - Jogador Congela

Correção parcial de um problema em que um anúncio não é reproduzido desde o início após a busca.

* Zendesk #17496 - Podbuster não é resolvido ao buscar de volta na janela do DVR

Forneça parâmetros personalizados para cada ad break.

**Versão 1.4.13** (1.4.13.660)

* Zendesk #4037 - Nenhum Erro de Perfil Utilizável (requer o Flash Player 18.0.0.232 ou superior)

corrigir problema de análise de url quando o parâmetro de consulta contém &quot;http&quot;

* Zendesk #4260 - o Flash Player 18 falha no IE11 (requer o Flash Player 18.0.0.232 ou superior)

Correção de uma falha ao reproduzir vídeo no modo de tela cheia com IE11

* Zendesk #4262 - O Adobe Primetime player trava no windows 10 (requer o Flash Player 18.0.0.232 ou superior)

Correção de uma falha ao reproduzir vídeo no modo de tela cheia com FireFox no Windows.

* Zendesk #4279 - Inserção de anúncio HLS TVSDK -302 problema de redirecionamento no iOS e Desktop

Correção de um problema em que um URL não obtinha seu tipo reconhecido corretamente porque não tinha extensão

* Zendesk #4306 - Falha no Flash Player ao entrar em tela cheia em Win apenas (requer Flash Player 18.0.0.232 ou superior)

Correção de uma falha ao reproduzir vídeo no modo de tela cheia no Windows.

* Zendesk #4480 - Eventos de tag ID3 ausentes (requer Flash Player 18.0.0.232 ou superior)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI e CRS | Aprimorar: trate elementos dinâmicos em determinados URLs de arquivo de mídia.

Serviço de reempacotamento criativo atualizado para lidar adequadamente com anúncios com URLs criativos dinâmicos.

* PTPLAY - 2114 - Suporte à reprodução de MP4.

A reprodução básica de conteúdo MP4 agora é compatível, incluindo reprodução, pausa e busca.

Os seguintes requisitos exigem o Flash Player 18.0.0.225 ou superior:

* Zendesk #3992 - Velocidades adicionais do TrickPlay.

O TrickPlay agora aceita taxas superiores a 16x: +/- 32, +/- 64 e +/- 128.

* Zendesk #3113 - Falha no plug-in do Flash Player

Correção de uma falha ao tentar reproduzir um anúncio de redirecionamento no Mac Firefox.

* Zendesk #4037 - Nenhum Erro De Perfil Utilizável
* Zendesk #4262 - falha no Adobe Primetime player no windows 10

Correção de uma falha no Windows Firefox durante a reprodução em tela cheia.

**Versão 1.4.11** (1.4.11.648)

* Zendesk #1869 - Problema ao Alterar Tamanho da Fonte (requer o Flash Player 18.0.0.200)

Permitir que os tamanhos de legenda sejam usados no código de legenda WebVTT.

* Zendesk #3113 - Falha no plug-in do Flash Player (requer o Flash Player 18.0.0.200)
* Zendesk #3268 - Desktop: O reprodutor de vídeo começa a piscar após +- 40/50 segundos e começa a ficar preto após +- 90 segundos (requer o Flash Player 18.0.0.200)

Corrigir bug de vídeo de estágio.

* Zendesk #3670 - erro INVALID_PARAMETER em VOD ao buscar no reprodutor de referência (requer o Flash Player 18.0.0.200)

InvalidateProfiles no ThreadSeek quando um novo período é detectado.

* Zendesk #3896 - Falha do Flash Player com Integridade de Fluxo definida como ATIVADO no Chrome (requer Flash Player 18.0.0.200)

Correção de uma falha no modo de rede nativo na pimenta

* Zendesk #3905 - O player TVSDK não carrega quando hospedado na CDN

Correção de problemas que encontravam um token curinga quando pageDomain era diferente do domínio swf.

**Versão 1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player trava Flash no Firefox

Correção de uma falha ocasional de Flash Player com o Firefox no Mac quando um fluxo, reproduzido em um monitor externo, alternava para um fluxo de taxa de bits mais alto.(requer Flash Player 18.0.0.160)

* Zendesk #3268 - Desktop: player de vídeo começa a piscar depois de `+-` 40/50 segundos e começa a ficar preto depois de `+-` 90 segundos

Correção de um problema no Mac Chrome em que o fluxo começava a cintilar e eventualmente ficava preto. (requer Flash Player 18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro não preenchida

   * o código de erro 400 será exposto se o anúncio em linha tiver criação incorreta.
   * `[ERRORCODE]` a macro será codificada em URL

* Zendesk #3601 - Solicitação de aprimoramento: Wrapper companion management

   * O TVSDK exibirá invólucros complementares que contêm recursos (html, iframe ou static ) fechados para o inline. (se o incorporado não contiver um para esse tamanho)
   * Os companheiros de invólucro com recurso, a menos que sejam usados para exibição, serão ignorados. (não é usado para rastreamento )
   * Somente companheiros de invólucro com NENHUM recurso serão usados para fins de rastreamento. ( companheiro de invólucro que contém apenas o rastreamento )

**Versão 1.4.9**

* Zendesk #2615 - problema ao remover a visualização HLS da exibição da área de trabalho

Adição do método clearVideo() ao MediaPlayer. Limpa o quadro de vídeo exibido, limpando o AVStream do objeto StageVideo. Só deve ser chamado se o vídeo estiver pausado, e replaceCurrentResource ou replaceCurrentItem precisar ser chamados antes que play() possa ser chamado novamente.

* Zendesk #3169 - Atualizar player de referência com a integração do Adobe Analytics

O reprodutor de referência foi atualizado com a integração do Adobe Analytics

* Zendesk #3296 - Desktop HLS TVSDK - Anúncios de terceiros VAST não reproduzidos

os tipos MIME para o formato HLS diferenciavam maiúsculas de minúsculas, isso estava incorreto e foi alterado para que não diferenciassem mais maiúsculas de minúsculas

**Versão 1.4.8**

* Zendesk #2737 - Desktop Player - Erro 106000 (requer Flash Player 17.0.0.184)
* Zendesk #3007 - Anúncios anteriores à exibição após a atualização para o Flash Player 17 (requer o Flash Player 17.0.0.184)
* Zendesk #3085 - Desktop HLS Player lança o erro 106000 após 60 segundos (requer o Flash Player 17.0.0.184)

**Versão 1.4.7**

* Zendesk #2760 - tag DISCONTINUITY ignorada durante o modo TrickPlay (requer o Flash Player versão 17.0.0.158)
* Zendesk #2760 - tag DISCONTINUITY ignorada durante o modo TrickPlay (requer o Flash Player versão 17.0.0.158)

**Versão 1.4.6**

* Zendesk #2652 - Documentação do Auditude para HLS de desktop, esclarecimento do Auditude media_id para documentação HLS de desktop

**Versão 1.4.5**

* Zendesk #2256 - Acesso à lista de reprodução Principal, PSDK atualizado para enviar eventos timedMetadata para tags assinadas na lista de reprodução principal. (requer o Flash Player versão 17.0.0.134)
* Zendesk #2417 - Player tentando baixar legendas antes do início da reprodução, WebVTT estava usando a variável de número de segmento errada para correspondência de número de segmento. O bug só era exibido para mídias que tinham índices de segmento começando em zero. (requer o Flash Player versão 17.0.0.134)
* Zendesk #2537 - Flash player trava ao usar o plug-in pimenta com Chrome (requer o Flash Player versão 17.0.0.134)
* Zendesk #2547 - Legendas árabes: o texto deve ser alinhado à direita justificado (requer o Flash Player versão 17.0.0.134)

**Versão 1.4.4**

* Zendesk #1561 - Re: `[Adobe Primetime]` Atualização: Suporte a failover baseado em cliente HLS para PROGRAM-DATE-TIME na PSDK do desktop (requer o Flash Player versão 16.0.0.305 ou superior)
* Zendesk #2197 - `[Ads]` Rastreamento de erros de anúncios
* Zendesk #2286 - Pedido em recursos: Fornecer informações sobre o status de carregamento do anúncio (VPAID)
* Zendesk #2285 - Solicitação de recurso: Ignorar anúncio após uma duração de tempo limite especificada
* Bug #3921755 - Atualização da biblioteca OpenSSL para a versão 1.0.1L no Flash Player (requer o Flash Player versão 16.0.0.305 ou superior)

**Versão 1.4.2**

* Zendesk #1303 - Deslocamento vertical para legendas ocultas (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento prevista: dezembro de 2014)
* Zendesk #1870 - Legendas ocultas ativadas e desativadas (requer o Flash Player versão 16.0.0.235 ou superior, data de lançamento prevista: dezembro de 2014)
* Zendesk #2110 - A reprodução fica paralisada após tentar entrar em tela cheia durante um anúncio VPAID (requer a versão do Flash Player 16.0.0.235 ou posterior, data de lançamento prevista: dezembro de 2014)
* Zendesk #2199 - `[VPAID]` O player não está respondendo ao buscar ad break passado
* Zendesk #2358 - Re: `[Analytics]` Dados de capítulo incorretos

**Versão 1.4.1**

* Atualização da API de Blecautes para manter a consistência com a implementação do Android e do iOS.

**Versão 1.4.0**

* Zendesk #1024 - Recurso para remover anúncio de transmissão via manifesto
* Zendesk #1423 - Falha de reprodução HLS está bloqueando o Flash Player (sem erro relatado)
* Zendesk #1674 - ClosedCaption Não aparece, corrija a exibição da legenda 708 quando os códigos ETX 0x03 estiverem ausentes.

## Problemas conhecidos {#known-issues}

* As Legendas ocultas não funcionarão com conteúdo somente de áudio porque o sistema de legendas precisa de vídeo para funcionar.
Sem o vídeo, não há dimensão de visor e, sem uma dimensão de visor, não é possível exibir gráficos para legendas.
* A integridade do fluxo é um pouco mais lenta no Google Chrome devido às restrições da sandbox do Chrome.
* No TVSDK 1.4, se você desativar a reprodução automática, um erro de DRM poderá ocorrer quando o reprodutor permanecer ocioso por pelo menos um minuto. Para contornar esse problema, ao desativar a reprodução automática, mas pré-carregar os ativos, modifique `ReferenceCore.as` alterando o conteúdo de `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versão 1.4.13** PTPLAY-8501 - Quando o VMAP retorna dois anúncios MP4 diretos não transcodificados, o mesmo anúncio de outono é reproduzido duas vezes.

* **Versão 1.4.2** Na versão 16 do Flash Player, um problema foi identificado com a lógica de &quot;switching down&quot; do ABR, depois que o reprodutor entra em um evento de buffering vazio. O problema impede que a taxa de bits seja desativada em ambientes de largura de banda ruim quando o player entrar em um estado de buffering. Para contornar o problema, defina o aplicativo como `BufferControlParameters.initialBufferTime` ser o mesmo que `BufferControlParameters.playbackBufferTime` temporariamente durante o estado de buffering (ou seja, em um `BufferEvent.BUFFERING_BEGIN` event) e redefina-a para os valores definidos em `BufferEvent.BUFFERING_END` evento. A correção para esse problema estará disponível na próxima versão de patch do Flash Player versão 16.

* **Versão 1.4.0**

   * PTPLAY-1634 - A mesma tag inscrita tem carimbos de data e hora diferentes em diferentes janelas ativas. Quando as janelas ativas são movidas, a mesma tag em cada uma delas deve ter os mesmos carimbos de data e hora. No entanto, às vezes, as mesmas tags têm carimbos de data e hora diferentes.
   * PTPLAY-28 - A linha do tempo do MediaPlayer não inclui quebras vazias.
   * É necessário um arquivo de política entre domínios (crossdomain.xml) para obter permissão para transmitir conteúdo de um domínio diferente. [Configurar um arquivo crossdomain.xml para transmissão HTTP](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html).
   * Bug #3694203 - Em um fluxo de DVR, buscar em um mid-roll de reprodução em outra sinalização de anúncio mid-roll pode levar ao congelamento do navegador
   * Bug #3753725 - selectPolicyForSeekIntoAd não leva em conta se o ad break foi assistido
   * Bug #3754529 - Os anúncios precedentes não são removidos do fluxo ao buscar de volta em um fluxo DVR ao vivo
   * Bug #3761896 - Se a busca for permitida durante a reprodução do anúncio, os marcadores de anúncio serão reajustados após a busca. A solução alternativa é não usar o retorno de chamada ITEM_UPDATED durante a busca
   * Bug #3779889 - A chamada completa não é feita ao chegar ao fim do truque de jogo no Video Analytics
   * Bug #VA-779 - A pulsação do evento de alteração da taxa de bits não é enviada para a Implementação de referência de suporte de heartbeat do Enhanced Video Analytics - A reprodução de truques não é implementada no aplicativo de amostra.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
