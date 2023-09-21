---
title: Notas de versão do TVSDK 1.4 para iOS
description: As Notas de versão do TVSDK 1.4 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK iOS 1.4
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6549'
ht-degree: 0%

---

# Notas de versão do TVSDK 1.4 para iOS {#tvsdk-for-ios-release-notes}

As Notas de versão do TVSDK 1.4 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK iOS 1.4.

## Novos recursos {#new-features}

**Versão 1.4.45**

* Para estar em conformidade com o Xcode10, o TVSDK mudou de &quot;`libstdc++`&quot; para &quot;`libc++`&quot; e, como resultado, a versão mínima compatível é a iOS 7. Anteriormente era o iOS 6.

**Versão 1.4.44**

* Nenhum recurso novo ou aprimoramento nesta versão.

**Versão 1.4.43**

* Experiência semelhante à de TV ao poder se associar no meio de um anúncio sem acionar o rastreamento de anúncios parciais.\
  Exemplo: o usuário se junta ao meio (a 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. São 10 segundos do segundo anúncio no intervalo.

   * O segundo anúncio é reproduzido pelo tempo restante (20 segundos) seguido pelo terceiro anúncio.
   * Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente para o terceiro anúncio são acionados.

* Adição da propriedade enableVodPreroll do tipo booleano na interface PTAdMetadata. A propriedade pode ser usada para ativar o pré-lançamento em um fluxo de VoD. Se enableVodPreroll for NO, o PSDK não reproduzirá antes da exibição. Isso, no entanto, não afeta os cilindros médios. O valor padrão de enableVodPreroll é SIM.
* A API closedCaptionDisplayEnabled da interface PTMediaPlayer é marcada como obsoleta do iOS v1.4.43 em diante. Para determinar se as legendas ocultas estão disponíveis para um determinado PTMediaPlayerItem, examine a propriedade subtitlesOptions de PTMediaPlayerMediaItem.

**Versão 1.4.42**

Nenhum recurso novo foi adicionado nesta versão. Para obter uma lista de problemas corrigidos, consulte Problemas resolvidos.

**Versão 1.4.41**

Alterações na API:

* **isSecure**: Uma nova API é introduzida no isSecure para proteger o reprodutor contra gravação e emissão de um erro. O valor padrão é true.
* **allowExternalRecording**: uma nova API é introduzida para permitir o espelhamento de reprodução automática para um conteúdo seguro. O espelhamento de reprodução é tratado como gravação, portanto, o valor allowExternalRecording deve ser definido como &#39;True&#39;, para permitir o espelhamento de reprodução ou definido como &#39;False&#39; para interromper o espelhamento de reprodução para conteúdo seguro. Por padrão, o valor é verdadeiro.

**Versão 1.4.40**

Sem novos recursos.

**Versão 1.4.39**

* O iOS TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.
* O iOS TVSDK foi atualizado para fazer solicitações do CRS do novo host do Akamai `primetime-a.akamaihd.net`.
* A nova configuração do nome de host fornece a entrega de ativos CRS por HTTP e HTTPS (SSL) em maior escala.

**Versão 1.4.36**

Integrar e certificar o VHL 2.0 no iOS TVSDK : reduza a barreira na implementação do VideoHeartbeatsLibrary diminuindo a complexidade das APIs.

**Versão 1.4.34**

* Informações sobre Anúncios de Rede

  As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. A ID do anúncio, o Sistema de publicidade e as Extensões de anúncios VAST são fornecidos em `PTNetworkAdInfo` classe acessível por meio de  `networkAdInfo`  em um ativo de anúncio. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como **Análise do Mat**.

**Versão 1.4.31**

* **Métricas de cobrança** Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.

Toda vez que o TVSDK gera um evento de início de fluxo, o reprodutor começa a enviar mensagens HTTP periodicamente para o sistema de cobrança do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

* **Suporte a várias CDNs para anúncios CRS** O TVSDK agora é compatível com vários CDNs para anúncios CRS. Ao fornecer detalhes de FTP para anúncios CRS, é possível especificar locais de CDN, diferentes do CDN padrão de propriedade de Adobe, como Akamai.

**Versão 1.4.29**

Na classe PTSDKConfig, a API forceHTTPS foi adicionada.

A classe PTSDKConfig fornece métodos para impor o SSL em solicitações feitas aos servidores do Adobe Primetime Ad Decisioning, DRM e Video Analytics. Para obter mais informações, consulte `forceHTTPS` e `isForcingHTTPS` nesta classe. Se um manifesto for carregado por HTTPS, o TVSDK preservará o uso de conteúdo do HTTPS e respeitará esse uso ao carregar qualquer URL relativo desse manifesto.

**Nota**: as solicitações para domínios de terceiros, como pixels de rastreamento de anúncio, URLs de conteúdo e anúncio e solicitações semelhantes, não são modificadas e é responsabilidade dos provedores de conteúdo e servidores de anúncio fornecer URLs compatíveis por meio de HTTPS.

**Versão 1.4.18**

O Primetime iOS TVSDK agora é compatível com criações JavaScript VPAID 2.0 para permitir uma experiência avançada de anúncios interativos em fluxo.

Para obter mais informações sobre o VPAID 2.0, consulte [Suporte a anúncios VPAID](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md).

**Versão 1.4.17**

* tvOS

  O TVSDK é compatível com aplicativos nativos tvOS.
* Os seguintes tipos de conteúdo podem ser reproduzidos:

   * VOD
   * Ao vivo
   * AES-128
   * Áudio e legendas alternativos
   * FER

* Os seguintes tipos de anúncios podem ser exibidos:

   * Básico
   * VAST2
   * VAST3
   * VMA

* Os seguintes recursos não são suportados no momento:

   * Digital Rights Management (DRM)
   * Banners de publicidade
   * Linguagem de Marcação da TV (TVML)

**Versão 1.4.13**

**Nota**: O módulo Nielsen foi removido da build do TVSDK. O TVSDK será atualizado em breve com um novo módulo de integração Nielsen.

* **Fallback de anúncios, encadeamento de Daisy na lógica de seleção de anúncios (Zendesk #3103)**

Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Fallback de anúncios para anúncios VAST e VMAP](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md).

**Versão 1.4.9**

* **Sinalização De Blecaute Com Substituição De Conteúdo Alternativo**

Como parte da atualização 1.4 do TVSDK, agora também oferecemos suporte à entrada e ao retorno de blecautes regionais em relação ao conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando a programação alternativa estiver sendo mostrada no lugar da programação original.

**Versão 1.4.8**

* **Biblioteca de Video Heartbeats (VHL) atualizada para a versão 1.5**

   * Capacidade de enviar metadados com início de vídeo e/ou início de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - As pulsações são menores em média e menores em tamanho

**Versão 1.4.7**

* **Suporte à individualização no local**

Suporte para instalações locais do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para ir para um endpoint diferente.

* **Proteção de saída baseada em resolução**

As Políticas DRM agora podem especificar a maior resolução permitida, dependendo dos recursos de Proteção de saída do dispositivo. Por exemplo: &quot;Se o HDCP estiver disponível, permita que o conteúdo com resolução de até 1080p seja reproduzido e, se o HDCP não estiver disponível, permita que o conteúdo com resolução de até 480p seja reproduzido&quot;.

**Versão 1.4.4**

* **Atualização da Biblioteca de vídeo Heartbeats (VHL) para a versão 1.4.1.1**

   * Adição da capacidade de reunir diferentes casos de uso de análise, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete. O ad break é inferido das chamadas de método trackAdStart e trackAdComplete.
   * A propriedade de indicador de reprodução não é mais necessária ao rastrear anúncios.
   * Adição de suporte para a ID de visitante do Marketing Cloud.

* **Integração do SDK Nielsen**

   * O TVSDK agora oferece suporte ao envio de beacons mTVR e MDPR ID3 para o SDK Nielsen, sem qualquer integração personalizada. Para começar, baixe o SDK de aplicativo 3.1.2.19 Nielsen iOS.

**Versão 1.4.0**

* **Sinalização De Blecaute Com Substituição De Conteúdo Alternativo**

   * Como parte da atualização do TVSDK 1.4, o TVSDK também oferece suporte à entrada e ao retorno de blecautes regionais em relação ao conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando a programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remova/substitua anúncios C3**

   * Agora, nenhum trabalho preparatório adicional é necessário para inserir dinamicamente novos anúncios nos ativos de vídeo sob demanda (VOD) que saem da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova e poderosa funcionalidade também é útil nos casos em que o conteúdo ao vivo/linear é transmitido e é imediatamente desativado para uso como conteúdo sob demanda sem o tempo adequado para &quot;limpar&quot; o ativo.

## Certificação e suporte a dispositivos na versão 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Os seguintes recursos são **não** compatível com o TVSDK:
>
>* Câmera lenta, em qualquer plataforma ou versão.
>* Jogo ao vivo.

**Versão 1.4.43**

* O TVSDK 1.4.43 é certificado para o iOS 11.

**Versão 1.4.29**

* O TVSDK 1.4.29 foi certificado para o iOS 10.

**Versão 1.4.28**

* O TVSDK 1.4.28 foi certificado para o iOS 10 Beta 7.
* Suporte DRM para forçar HTTPS adicionando as APIs forceHTTPS e isForcingHTTPS.
* As bibliotecas do VHL foram atualizadas para 1.5.8, as bibliotecas do Adobe Mobile foram atualizadas para 4.8.4 e a biblioteca do utilitário logger foi atualizada para a versão 7.0 do target de implantação.

**Versão 1.4.19**

Esta versão do TVSDK foi certificada com o FairPlay Support para iOS e tvOS.

**Versão 1.4.17**

* tvOS

  Esta versão do TVSDK inclui suporte para tvOS e foi certificada para fluxos HLS não criptografados.

  **Nota**: Lembre-se das seguintes diretrizes de compilação:

   * O suporte para tvOs TVSDK é limitado a fluxos criptografados não DRM de Adobe. Você deve remover a referência a drmNativeInterface.framework nas configurações de build do tvOS. Os fluxos criptografados AES ainda são compatíveis.
   * O Apple exige que todos os aplicativos da Apple TV sejam habilitados para código de bits, portanto, você deve ativar esse sinalizador nas configurações do projeto.

## Problemas resolvidos no 1.4 {#resolved-issues-in}

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
-->

<!-- 

Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 

-->

**Versão 1.4.45{#ios-tvsdk}**

* Ticket #36294 - o TVSDK da iOS não funciona com o Xcode 10

   * Correção de problemas de compilação com TVSDK no XCode 10. Devido aos requisitos do XCode 10, os aplicativos criados no TVSDK para iOS 1.4.45 em diante exigem o direcionamento mínimo de implantação como o iOS 7.0

* Ticket #36321 - Discrepância observada no intervalo pesquisável entre a ocorrência de PTMediaPlayer e AVPlayer no estado &quot;Reproduzindo&quot;.
* Ticket #36493 - `libstdc++` suporte no iOS 12

   * Correção de problemas de compilação com o TVSDK no iOS 12. Os aplicativos criados com o TVSDK para iOS 1.4.45 em diante exigem o direcionamento mínimo de implantação como o iOS 7.0

**Versão 1.4.44**

* Ticket #34683 - O Tempo De Progresso Da Reprodução Do Anúncio Está Indo Negativo

   * Verificações adicionais são colocadas para lidar com o caso quando há uma incompatibilidade entre a duração relatada pelo servidor de publicidade e o conteúdo real do anúncio.

* Ticket #34801 - currentTime e localTime não estavam sendo atualizados ao procurar uma nova posição durante o status pausado

   * A hora atual do player agora pode ser definida como zero caso o player esteja no estado pausado; anteriormente, a hora atual costumava ser definida como zero somente no estado de reprodução.

* Ticket #35037 - a reprodução é interrompida com um URL incorreto ao retornar da inserção de anúncio baseado em sinal.

   * Correção aprimorada fornecida para o problema fechado #34385 na versão 1.4.42. Adição do código de controle de verificação e exceção isCancelled para tornar a fila de operações mais robusta.

**Versão 1.4.43**

* (ZD#32990) - iOS: reprodução de conteúdo em vez de anúncios em alguns pontos de sinalização. A API &quot;seletedMediaOptionInMediaSelectionGroup&quot; que fazia parte da interface AVPlayerItem agora foi movida para AVMediaSelection no iOS 11. O problema foi resolvido usando essa nova API.
* (ZD#33683) TVSDK removido == sufixo das cadeias de caracteres de metadados. O problema é corrigido na lógica de análise.
* (ZD#33905) - iOS TVSDK que faz chamadas para os arquivos manifest com dois agentes do usuário. O problema do agente do usuário foi corrigido na primeira chamada m3u8 (novo caso de instalação). As M3u8 têm os mesmos user-agents para todas as chamadas agora.
* (ZD#34293) - Os pré-rolagens inseridos em fluxos LINEARES não são reproduzidos corretamente no iOS11. O problema é corrigido para anúncios precedentes.
* (ZD#34684) - Quando a política de ignorar anúncio é aplicada, os quadros de anúncio anteriores à exibição são exibidos por alguns segundos. Uma nova API, enableVodPreroll, foi introduzida para desativar a reprodução de pré-rolagem na reprodução de vod. O valor padrão para essa API é &#39;Sim&#39;. A API garante que a compilação de conteúdo de anúncios seja ignorada no conteúdo principal.
* (ZD#34765) - Depois de chamar stop(), alguns segmentos de Fluxos de Transporte ainda são baixados. API Stop() aprimorada para evitar o download de segmentos extras.
* (ZD#34865) - Os anúncios precedentes para a transmissão em tempo real estão truncados no iOS. Relacionado ao iOS11, e a adição de uma verificação adicional para confirmar se o fluxo é pré-lançamento ou conteúdo principal resolve esse problema.
* (ZD#35093) - Corrigido um cenário de failover em que, se a variante principal do fluxo falhar na inicialização (retorna 404), a reprodução não alternará para o fluxo de backup.

**Versão 1.4.42 (1.4.42.118)**

* (ZD#34385) - A reprodução é interrompida com um URL inválido ao retornar da inserção de anúncio baseada em sinal.

  Aumente o máximo de contagens simultâneas para CustomAVAssetLoaderOperations, para que as leituras de manifesto possam continuar a ser executadas.
* (ZD#34373) - Os usuários finais não podem fazer streaming para dispositivos conectados a HDMI, quando a gravação de stream não é permitida.
* (ZD#32678) - O TVSDK não coleta as IDs de anúncios corretas no iOS.

  A ID do anúncio final do criativo agora é escolhida nos pings do VHL no caso de redirecionamentos VAST/VMAP.
* (ZD#33904) - O TVSDK não está Registrado para notificações do AVFfoundation AVAudioSessionMediaServicesWereLostNotification e AVAudioSessionMediaServicesWereResetNotification.

  PTMediaServicesWereLostNotification e PTMediaServicesWereResetNotification agora podem ser registrados no aplicativo do player para receber as notificações quando os serviços de mídia são redefinidos ou perdidos.

* (ZD#33815) - Os clientes não conseguem atualizar suas regras de priorização e normalização do CRS sem exigir uma atualização do aplicativo.

  Adicionadas as APIs getCRSRulesJsonURL e setCRSRulesJsonURLs ao iOS TVSDK.

**Versão 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemas de criação do aplicativo de referência com o TVSDK versão 1.4.41

  A partir desta versão, o Xcode 9 é necessário para compilar o TVSDK para iOS.
* (ZD #29456) - Início da reprodução no estado pausado

  Correção do problema de pausa que ocorre quando o vídeo é pausado ao entrar na reprodução.
* (ZD #30371) - A hora de início do AdBreak muda quando inserimos mais de 2 anúncios em fluxo linear

  Correção do erro ao tentar reproduzir conteúdo na Apple TV, o que impedia a reprodução por completo
* (ZD #32146)- Nenhum PTMediaPlayerStatusError é recebido para conteúdo HLS Live no bloqueio do iOS 11 dev beta

  Nenhum PTMediaPlayerStatusError é recebido para conteúdo HLS Live e VOD no bloqueio usando o Charles (Desconectar conexão e 403)
* (ZD #29242) - A reprodução do vídeo Airplay falha com os anúncios ativados

  Quando os anúncios estão ativados e o AirPlay está ativado ao iniciar a reprodução de um vídeo, a reprodução nunca é iniciada e nenhum erro é exibido
* (ZD#33341) - DRMInterface.h aciona avisos de criação no Xcode 9

  Correção de dois protótipos de bloco no DRMInterface.h que não tinham a palavra &#39;void&#39; em suas listas de parâmetros
* (ZD#31979) - Não compila/executa quando é iOS 10 ou posterior para iPhone 7/iPhone7+

  A compilação fixa de documentos IB para versões anteriores ao iOS 7 não é mais suportada
* (ZD#32920) - Tela em branco dentro de um Ad break e sem conclusão de Ad break

  Quando um Ad break está apresentando instâncias de Anúncio e após a conclusão de uma instância de anúncio, uma tela em branco é exibida
* (ZD#32509) - Desative o iOS 11 screen recoding Desative a gravação de tela no iOS 11

* (ZD#33179) - Falha de evento intermitente no iOS11

  Correção da falha de evento no iOS 11

**Versão 1.4.40** (1.4.40.72)

* (ZD #32465) - O player não pode manipular listas de reprodução mescladas.

  Chame finishLoadingWithError(with: Error) para que o AV Foundation tente failover alternativo de fluxos/disparador.

* (ZD #31951) - Erro de TVSDK durante rotações de licença.

  Correção do problema de rotação de licenças.
* (ZD #31951) - Tela em branco dentro de um Ad break e sem conclusão de Ad break.

  Foi tratado um problema em que os anúncios VPAID do Facebook frequentemente retornavam vários blocos CDATA em um único nó \&amp;lt;AdParameters\&amp;gt; VAST.
* (ZD #33336) - [iOS] TVSDK - Os pods de anúncios não estão sendo preenchidos, apesar de anúncios suficientes serem retornados pelo Freewheel.

  Relação pai-filho criada entre o anúncio de sequência e o anúncio de fallback e classificação com base na sequência e no índice pai.

**Versão 1.4.39** (1.4.39.43)

* (ZD #32178) - A versão do iOS TVSDK está incorreta.

  A saída da versão do TVSDK nos arquivos de log foi 1.0.211. Correção da saída da versão correta.

* (ZD #32199) - Carregamento lento de anúncio - O vídeo não é exibido para o conteúdo.

  A linha do tempo local do Adbreak que não estava sendo inicializada anteriormente, foi atualizada antes de ser usada.

* (ZD #27528) - O vídeo, áudio ou ambos congelam de 1 a 45 segundos após um ativo começar a ser reproduzido, se o áudio secundário estiver definido como não padrão no iOS 1.2.

  Prepare e informe faixas de áudio no estado Pronto.

* (ZD #30411) - Você pode obter resultados inesperados, como ausência de áudio ou áudio incorreto, se escolher um idioma Sap secundário.

  Prepare e informe faixas de áudio no estado Pronto.

* (ZD #32199) - Carregamento lento de anúncio - O vídeo não é exibido para o conteúdo.

  A linha do tempo local do Adbreak que não estava sendo inicializada anteriormente, foi atualizada antes de ser usada.

* (ZD #27528) - O vídeo, áudio ou ambos congelam de 1 a 45 segundos após um ativo começar a ser reproduzido, se o áudio secundário estiver definido como não padrão no iOS 1.2.

  Prepare e informe faixas de áudio no estado Pronto.

* (ZD #30411) - Você pode obter resultados inesperados, como ausência de áudio ou áudio incorreto, se escolher um idioma Sap secundário.

  Prepare e informe faixas de áudio no estado Pronto.

**Versão 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Adicionar AdSystem e Creative Id às solicitações do CRS

Uso de ID criativa e AdSystem na solicitação CRS com base nas regras de normalização CRS

* (ZD #29176) - Falha em PTAdPolicyDeligate satAdBreakAsWatched:position

A falha devido ao AdBreak vazio foi tratada agora.

* (ZD #30125) - Anúncios programáticos não estão funcionando na plataforma iOS

Adição de suporte a anúncios programáticos no iOS.

* (ZD #30782) - Notificação #EXT-X-PROGRAM-DATE-TIME

O evento de metadados cronometrado não é acionado para a tag # EXT-X-PROGRAM-DATE-TIME com fluxos DRM AO VIVO.

**Versão 1.4.37 (1.4.37.842)**

* (ZD #28950 ) - Problema de reprodução de VOD

Problema de reprodução quando a tag # EXT-X-PLAYLIST-TYPE no fluxo é definida como Evento em vez de VOD

* (ZD #29281) - iOS: Adicionar AdSystem e Creative Id às solicitações do CRS

Uso da Creative Id e do AdSystem na solicitação do CRS com base nas regras de normalização do CRS.

* (ZD #29462) - Anúncio do TremorHub em A&amp;E VOD causando uma falha nos aplicativos da iOS

**Versão 1.4.36 (1.4.36.835)**

* (ZD #29418) - Dicas com duração 0 (#EXT-X-CUE-OUT:0.000) estão fazendo com que o iOS TVSDK pare ou trave a reprodução.

O problema é corrigido e a reprodução começa corretamente.

* (ZD #29462) - Anúncio em VOD causando uma falha no iOS TVSDK .

O problema foi corrigido. O iOS TVSDK está gerando uma exceção (AUDNetworkAdInfo::initWithAdId) e não está lidando com ela. A exceção se deve à ID vazia do anúncio.

* (ZD #29281)- Adicione o AdSystem e a Creative id às solicitações do CRS.

Inclua AdSystem e CreativeId como novos parâmetros nas solicitações 1401 e 1403 (todos os outros parâmetros permanecem os mesmos).

**Versão 1.4.35** (1.4.35.830)

* (ZD #27830) - Precisa determinar programaticamente a diferença entre legendas ocultas e legendas no iOS.

O TVSDK agora expõe os dois tipos que podem ser usados para filtrar o tipo de legenda necessário.

* (ZD #29160) - As dicas de anúncios EXT-X-CUE-OUT não são empacotadas corretamente no TVSDK iOS.

Com EXT-X-CUE-OUT midroll anúncio está sendo reproduzido agora.

* (ZD #29100) - O aplicativo trava quando o usuário movimenta até o final de um filme.

Correção de várias falhas relacionadas à sincronização.

* (ZD #28785), (ZD #27712) e (ZD #25076) - O aplicativo iOS falha durante os grandes eventos ao vivo.

Correção de várias falhas relacionadas à sincronização.

**Versão 1.4.34** (1.4.34.815 para iOS 6.0+)

* (ZD# 28481) - Interrupção do FER devido à anexação da chave incorreta ao final de um ad break para esses fluxos de FER

Para um fluxo FER, a chave antes do ad break é inserida após o fim do ad break. Esse problema foi resolvido anexando o *última chave vista* no fim do ad break.

**Versão 1.4.33** (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Habilitar CRS para Subcontas

Ativado ao enviar o URL criativo original para a solicitação do CRS 1401 em vez do URL normalizado, de acordo com o requisito para o back-end do CRS.

* (ZD# 26218) - PSDKResources.bundle carregando problema

Esse problema foi resolvido atualizando o carregamento de recursos para procurar em todos os pacotes disponíveis.

* (ZD# 27460) Primeira chamada de anúncio Midroll - POST para cdn.auditude<span></span>.com retornando 403.

A nova conta CDN não pode lidar com uma solicitação CDN POST. Esse problema foi resolvido atualizando o código para fazer o `cdn.auditude.com` solicitação de anúncio para ser GET em vez de POST.

**Versão 1.4.32** (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Suporte para valores decimais para quebras de anúncios VMAP.

Quando o conteúdo não era segmentado ao longo dos ad breaks definidos, os números inteiros estavam causando posicionamentos de anúncios inesperados. O problema foi resolvido sem converter os valores decimais em números inteiros.

* (ZD# 27189) O conteúdo AES com a tag EXT-X-DISCONTINUITY-SEQUENCE não está sendo reproduzido corretamente.

O problema foi resolvido colocando a tag no início da lista de reprodução.

**Versão 1.4.31** (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar Métricas de Uso do TVSDK para Faturamento

Para obter mais informações, consulte [Métricas de cobrança](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md).

* (ZD# 24642) Suporte Picture-in-Picture para TVSDK

O recurso picture-in-picture, que não funcionava corretamente em alguns casos, foi corrigido.

* (ZD# 25246) Sinais De Ad Break Incorretos

Esse problema foi resolvido alinhando tags de descontinuidade em manifestos de variante.

* (ZD# 26218) O processo de compilação do aplicativo fica complicado ao tentar incluir PSDKLibrary.framework na estrutura do aplicativo do cliente

Esse problema foi resolvido empacotando o PSDKLibrary.framework conforme solicitado.

* (ZD# 26364) Suporte a vários CDNs para anúncios CRS
<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Atraso na reprodução de alguns fluxos no iOS 10.

Esse problema foi resolvido fornecendo uma solução alternativa para fluxos que não têm uma extensão M3U8.

**Versão 1.4.30** (1.4.30.754 para iOS 6.0+)

Os seguintes problemas foram resolvidos para TVSDK nesta versão:

* (ZD# 24180) Adicionar um cabeçalho personalizado ao lista de permissões

Um novo cabeçalho personalizado foi adicionado à lista de permissões TVSDK.

* (ZD# 25016) O fluxo de failover é selecionado aleatoriamente quando os parâmetros de controle ABR são definidos

Esse problema era resolvido mantendo os fluxos ABR em ordem quando as configurações ABR eram fornecidas com a configuração initialBitrate em um fluxo que inclui URLs de failover. Isso evitará a reprodução dos fluxos de failover em vez dos primários.

* (ZD# 25076) Falha em PTAuditudeAdResolver loadComplete

O problema em que uma falha ocorria durante o início/término rápido de várias instâncias do PTMediaPlayer com anúncios foi corrigido.

* (ZD# 25960) Nenhuma tag adicional assinada está acionando difusões de notificação de alteração de metadados

O problema em que uma tag assinada não é notificada quando aparece antes que o primeiro segmento no manifesto tenha sido corrigido.

* (ZD# 26084) PSDK lançando um 106000.101000.Erro -11833 decodificador não encontrado ao fazer a transição do último ad break para conteúdo de entretenimento

Quando o último tempo de início de ad break do VMAP cai antes da duração total ser concluída, em determinadas condições, a chave não é inserida até o final do último ad break. Esse problema foi corrigido.

* A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

   * (ZD #22351) VHL - Analytics: duração do ativo de vídeo ao vivo

Esse problema foi resolvido adicionando a API assetDuration a `PTVideoAnalyticsTrackingMetadata` para atualizar a duração do ativo para fluxos ao vivo/lineares e fornecer uma lógica para verificar o fluxo ao vivo.

* (ZD# 22675) VHL - Analytics: atualização da duração do ativo de vídeo ao vivo

Este problema é o mesmo que ZD #22351.

* (ZD #25908) VHL - Analytics: Falha no evento do Adobe Heartbeat

Esse problema foi resolvido com a atualização da implementação para usar a versão mais recente do VHL para iOS versão 1.5.9 para melhorar a estabilidade e o desempenho.

* (ZD #25956) VHL - Analytics: falha ao reproduzir vídeos repetidamente

Este problema é o mesmo que ZD #25908.

**Versão 1.4.29** (1.4.29.743)

* (ZD# 23901) Anúncios de terceiros não estão sendo reproduzidos

Esse problema foi resolvido movendo-se para a estrutura de URL do CRS v3 para incluir a ID da região no URL reempacotado.

* (ZD #25183) Problemas com a reprodução DRM no tvOS e no iOS

Esse problema foi resolvido fornecendo suporte para várias tags principais necessárias para suporte a vários DRMs.

* (ZD# 25334) Falha do TVSDK ao reproduzir um conteúdo compartilhado cDVR

Esse problema era resolvido evitando que o TVSDK convertesse cadeias de caracteres vazias em URLs absolutas.

* (ZD# 25347) Definir cabeçalho HTTP personalizado no AVURLAsset

Foi adicionado suporte para cabeçalhos personalizados em solicitações de segmentos ts por meio da classe PTNetworkConfiguration.

**Versão 1.4.28** (1.4.28.722)

* (ZD #24549) Várias chamadas de rastreamento de anúncios

Esse problema foi resolvido atualizando o gerenciador de linha do tempo para acompanhar as notificações em um objeto específico quando vários players são criados.

* (ZD #24758) O PTManifestLogger não é compatível com o iOS 8

Esse problema foi resolvido atualizando a biblioteca do utilitário logger para o destino de implantação da versão 7.0.

* (ZD #24775) Fluxo atrasado devido a Anúncios

Esse problema foi resolvido calculando corretamente a variação de duração nas listas de reprodução do evento.

* (ZD #24799) Alguns episódios não estão sendo reproduzidos no iOS APP

Esse problema era resolvido usando o servidor Web local para legendas quando os arquivos WebVTT eram geo-restritos.

**Versão 1.4.27** (1.4.27.711) para iOS 6.0+

* (ZD #24089) - Otimizações para resolução de anúncios em fluxos DVR longos

Esse problema foi resolvido adicionando várias otimizações para reduzir o tempo necessário para processar a janela do DVR em fluxos ao vivo/lineares.

* (ZD #21554) - Os beacons de erro do TVSDK não são acionados para o tipo de aplicativo = video/mp4

Esse problema foi resolvido permitindo que o reprodutor execute ping nos URLs de rastreamento de erros corretos em formatos de ativos inválidos.

* (ZD #24424) - Falha do tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS originada de dentro do PSDKLib para iOS em dispositivos de hardware mais recentes.

A falha que ocorria por causa de uma instância de reprodutor de mídia desalocada, quando a reprodução é alternada rapidamente entre fluxos diferentes, foi corrigida.

* (ZD #24575) - Falha no TVSDK em dispositivos de 32 bits quando enableDebugLog=true

O problema no formato de log que causava a falha em dispositivos de 32 bits quando o registro era ativado foi corrigido.

**Versão 1.4.26** (1.4.26.702) para iOS 6.0+

* (ZD# 20213) - O FW TVSDK precisa ser dinâmico/modularizado para XCode7

   * Corrigido ao atualizar as bibliotecas com suporte ao módulo

**Versão 1.4.25** (1.4.25.684) para iOS 6.0+

* (ZD #19629) - Pausa de vídeo ao vivo ao entrar no Airplay para ATV 4

Esse problema foi resolvido adicionando um período de espera após a remoção de itens antigos, mas antes de adicionar novos itens ao AVQueuePlayer. Sem o período de espera, as notificações são enviadas ao item incorreto.

* (ZD #19856) - Nenhuma legenda é exibida quando habilitada por padrão

Os problemas na lista de reprodução de webvtt, que fazia com que as legendas não fossem exibidas corretamente, foram corrigidos.

* (ZD #21590) - Desempenho e rastreamento de vídeo nas compilações de origem mais recentes

O problema sobre a duração do vídeo ausente no VideoAnalytics foi corrigido.

* (ZD #20202) - A definição do estilo de legendas personalizadas falha o aplicativo iOS

Esse problema foi resolvido adicionando verificações de objeto nulo ao definir estilos de legenda.

* (ZD #20709) - duração do vídeo relatada como 0 no rastreamento de início de vídeo

Este problema é o mesmo que (ZD #21590).

* (ZD #22280) - Duração de vídeo do Analytics definida como 0

Este problema é o mesmo que (ZD #21590).

* (ZD #22592) - Problemas com o Airplay no Primetime

Este problema é o mesmo que (ZD #19629).

* (ZD#22922) - Alternância manual da taxa de bits para o iOS

Esse problema foi resolvido fornecendo uma opção para especificar a taxa máxima de bits.

* (ZD #23084) - conformidade da Apple para redes somente IPv6

Os símbolos que não foram recomendados pelo Apple para compatibilidade IPv6 foram removidos.

**Versão 1.4.24** (1.4.24.661) para iOS 6.0+

* ZD #2548) - Suporte do Primetime para publicidade interativa em dispositivos móveis - VPAID 2.0

Esse problema era resolvido atualizando a lógica para mostrar a exibição do player se um anúncio VPAID falhasse na reprodução.

* (ZD #20101) - A implementação de capítulo personalizado aciona o evento de início de capítulo durante a reprodução de anúncio

Esse problema foi resolvido atualizando o VideoAnalyticsTracker para detectar corretamente o início/término do capítulo ao fazer a transição entre limites de capítulo e não capítulos.

* (ZD #20784) - Analytics: o acionamento de conclusões de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido adicionando uma lógica para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo.

As seguintes bibliotecas foram atualizadas:

* Biblioteca do AdobeMobile para 4.10.0
* Biblioteca do VHL para 1.5.6
* Biblioteca VHL-Nielsen para 1.6.7
* (ZD #21855) - As legendas não são reproduzidas após o lançamento

Nesse problema, as tags de descontinuidade duplicadas faziam com que as legendas não aparecessem depois do meio da exibição. Esse problema foi resolvido removendo as tags de descontinuidade que estão próximas umas das outras.

* (ZD #21994) - String fora dos limites em PTHLSUtils

A causa mais provável da falha é quando um EXT-X-KEY tem um URL entre aspas.

* ZD #22074) - Falha de AUDVAST ocorrendo uma vez por minuto no iOS

Na versão 1.4.23, a falha causada pela presença de caracteres inseguros em um URL de redirecionamento VAST foi corrigida. No entanto, o TVSDK continuava ignorando esses anúncios.

Esse problema foi resolvido ao manipular os caracteres inseguros e permitir que os anúncios fossem reproduzidos.

* (ZD #22694) - PTMediaPlayer.  A visualização está oculta pelo reprodutor

Esse problema era resolvido atualizando a lógica para mostrar a exibição do player se um anúncio VPAID falhasse na reprodução.

**Versão 1.4.23** (1.4.23.641) para iOS 6.0+

* (ZD #18016) - Nenhuma resposta do SDK do Primetime com uma condição de rede incorreta

Esse problema foi resolvido melhorando a notificação de erro quando ocorria um erro fatal do AVFFoundation e permitindo que o aplicativo manipulasse a reinicialização após o erro.

* (ZD #20580) - Falha no PTSplicerManager

Esse problema foi resolvido fornecendo proteção adicional contra problemas de simultaneidade que causam a falha.

* (ZD #21782) - Código de erro iOS 10100

O problema em que o TVSDK retornava um erro 101000 ao iniciar a reprodução em fluxos DRM de acesso ao Adobe foi corrigido.

* (ZD #21889) - Anúncios online e falha na reprodução de conteúdo offline

O problema em que a reprodução falhava após um anúncio no conteúdo offline criptografado do AES ter sido corrigido.

* (ZD #22074) - Falha de AUDVAST acontecendo uma vez por minuto no iOS

Esse problema foi resolvido melhorando o tratamento de tags de anúncios VAST de terceiros que têm caracteres inválidos no URL.

* (ZD #22257) - O TVSDK não reproduz o fluxo DRM

O problema em que o TVSDK que retornava um erro 101000 ao iniciar a reprodução nos fluxos DRM de acesso ao Adobe foi corrigido.

**Versão 1.4.22** (1.4.22.627) para iOS 6.0+

* (ZD #18709) - Falha no TVSDK para iOS

O problema de travamento em alguns fluxos protegidos por DRM de acesso de Adobe foi corrigido.

* (ZD #18850) - Atualizar a lógica de seleção criativa com base nas regras CRS

Esse problema foi resolvido adicionando um arquivo de configuração .json para especificar a prioridade da seleção criativa.

* (ZD #19770) - Feed de vídeo AES protegido não é mais reproduzido

O problema em que determinados fluxos redirecionados 302 não eram reproduzidos foi corrigido.

* (ZD #19629) - Pausa de vídeo ao vivo ao entrar no Airplay para ATV 4

Esse problema foi resolvido adicionando uma solução alternativa para a pausa de vídeo ao vivo quando o airplay é ativado para dispositivos Apple TV 4. O problema parece ser um problema da Apple TV 4.

* (ZD #21119) - O TVSDK é paralisado após a reprodução do anúncio

Foi adicionado suporte para fluxos criptografados AES com uma sequência IV ao usar a inserção de anúncio.

* (ZD #21125) - Retorno antecipado de ad break dinâmico/linear

Foi adicionado suporte para retornar de um ad break antes que o ad break seja reproduzido até a conclusão. O retorno antecipado é indicado por meio de uma tag de manifesto personalizada.

* (ZD #21224) - Suporte a airplay para fluxos tokenizados do Akamai

As APIs foram adicionadas à classe PTNetworkConfiguration para anexar cookies como parâmetros de URL em segmentos para determinados fluxos tokenizados do Akamai.

* (ZD #21287) - Log Irrelevante

Um problema com algumas instruções de log mostradas por padrão no console xcode, mesmo quando o registro está desativado, foi corrigido.

* (ZD #21446) - Eventos de ad break às vezes não acionados pelo TVSDK

Nos fluxos de EVENTO, as ad breaks não são acionados corretamente na build da versão anterior. Esta build aborda esse problema.

**1.4.21** (1.4.21.605) para iOS 6.0+

* (ZD #20749) - O fallback ignora respostas VAST não vazias; URLs de rastreamento de anúncios extras são acionados

Um problema com pings duplicados em anúncios de fallback foi resolvido.

**1.4.20** (1.4.20.590) para iOS 6.0+

* (ZD #18639) - O TVSDK está usando CPU/recursos em excesso em um ativo de gravação lenta

O uso excessivo de CPU/recursos foi corrigido nos dois níveis. Primeiro, permitindo que a função de atualização de tempo seja executada em uma fila global, em vez da thread principal, e otimizando o uso da CPU para analisar o manifesto com o m3u8 processado e armazenado em cache anteriormente.

* (ZD #19349) - Os anúncios precedentes estão sendo ignorados ao limitar a conexão de rede.

Esse problema foi resolvido fornecendo um evento de tempo limite (requestTimeout) ao aplicativo e ao adMetadata.  API adRequestTimeout para substituir o tempo limite padrão de 10 segundos.

* (ZD #19446) - Notificação ausente em fluxos ao vivo

Esse problema foi resolvido permitindo que o aplicativo assinasse EXT-X-PROGRAM-DATE-TIME em transmissões em tempo real.

* (ZD #19459) - Falha ao preparar áudio alternativo com PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Falha - [PrepareSubtitlesOptionsWithAVMediaSelectionOptions de PTMediaPlayerItem:nonForcedOptions:]

Esta edição é a mesma do Zendesk #19459.

* (ZD #19574) - O TVSDK não está retornando dados de resposta do M3U8 para conteúdo DRM ou não DRM

No carregamento inicial do arquivo de manifesto em PTMediaPlayerItem.prepareToPlay, se o carregamento do manifesto falhar, o TVSDK não relatará o corpo da resposta de falha para o aplicativo.

Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro ao aplicativo.

* (ZD #19615) - A lógica de fallback não está funcionando

Na implementação atual, os anúncios de fallback foram ignorados e não foram empacotados novamente, a menos que esses anúncios estejam no formato m3u8. Esse problema foi resolvido adicionando também o suporte ao reempacotamento de anúncios de fallback.

* (ZD #19770) - O TVSDK não reproduz nenhum conteúdo AES protegido com redirecionamento 302

O problema de redirecionamento foi corrigido porque a URL de redirecionamento estava sendo apagada por cleanConnectionData antes de poder ser usada para analisar o manifesto.

* (ZD #19856) - As legendas não são exibidas para algumas taxas de bits quando ativadas por padrão

Esse problema foi resolvido com a manipulação do erro do iOS para os segmentos dos fluxos nos quais as legendas não são exibidas.

* (ZD #19868) - O TVSDK trava quando um criativo inválido é traficado

A falha no TVSDK que estava desalocando incorretamente uma instância do vasto analisador foi corrigida.

* (ZD #20180) - Anúncios VPAID são ignorados ocasionalmente

O tipo mime do JavaScript nem sempre foi incluído ou considerado um tipo mime válido. Esse problema foi resolvido incluindo o JavaScript como um tipo MIME válido.

* (ZD #20749) - O fallback ignora respostas VAST não vazias; URLs de rastreamento de anúncios extras são acionados

O problema em que algumas criações não estão sendo reembaladas foi corrigido.

**Versão 1.4.19** (1.4.19.563) para iOS 6.0+

* ZD #18639) - O TVSDK usa recursos/CPU excessivos em um ativo de gravação lenta

Esse problema foi resolvido com a otimização da regravação da lista de reprodução DRM m3u8 para bits de cache da lista de reprodução que foram regravados anteriormente. Isso é mais relevante quando você reproduz fluxos de m3u8 ao vivo para os quais o m3u8 é baixado após cada download de segmento.

* (ZD#18956) - player.drmManager é nil quando o ponto de interrupção é definido no iOS Demo Player

Esse problema foi resolvido atualizando a implementação da API PTMediaPlayer.drmManager para coletar o DRManager da estrutura DRM.

**Versão 1.4.18** ( 1.4.18.557) para iOS 6.0+

* (ZD #18844) Rastreamento do indicador de reprodução do conteúdo ao vivo no iOS player.

Esse problema foi resolvido permitindo que os aplicativos definissem seu próprio valor de indicador de reprodução.

* Zendesk #18518 - Se o nome do vídeo não for especificado, o nome do TVSDK assumirá como padrão *Reprodutor baseado em PSDK.*

Esse problema foi resolvido com a remoção do valor padrão para o nome do reprodutor.

**Versão 1.4.17** (1.4.17.545) para iOS 6.0+

* Zendesk #2228 - Aprimorar o TVSDK para retornar a resposta JSON da busca de um manifesto

Em vez de enviar um erro quando o conteúdo não é M3U8, o DRM Framework retorna um DRMetadata nil. O problema era resolvido adicionando metadados para expor conteúdo quando a notificação M3U8_PARSER_ERROR ocorria.

* Zendesk #2231 - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification

Mesma resolução que Zendesk #2228

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro não preenchida

O problema em que o SDK do Auditude não envia um ping quando o URL de rastreamento tem espaços no início foi resolvido.

* Zendesk #17294 - Falha SecKeyRawSign

Uma possível falha quando o código do cliente usa o conjunto de chaves foi resolvida.

* Zendesk #18008 - Cookies de suporte para iOS8+ para suportar fluxos tokenizados

Fluxos tokenizados do Akamai exigem que os cookies sejam enviados em solicitações de segmento, e isso não foi possível no iOS 7 e versões anteriores. A partir do iOS 8, a Apple adicionou uma API que permite que os cookies sejam transmitidos para solicitações de segmento. Esse suporte agora está disponível no TVSDK. Também foi adicionado suporte para enviar um user-agent, se disponível.

* Zendesk #18166 - TVSDK 1.4.15 fornece centenas de avisos ao compilar com o DWARF com opções de arquivo dSYM

Todos os avisos foram resolvidos.

**Nota**: bibliotecas compatíveis com tvOS foram adicionadas para TVSDK .

**Versão 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S Trava durante a reprodução

Revertendo a dependência do OKHTTP na auditoria para CRS porque o TVSDK agora está usando diretamente a conexão httpurl em vez de curl. O problema foi resolvido limpando as exceções antes de fazer outra chamada JNI.

* Zendesk #4487 - Rastreamento do canal linear de conteúdo

O problema foi resolvido ao reinicializar o rastreador de heartbeat de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17919 - Android - A busca de conteúdo causa erro de heartbeat

O problema era resolver a pulsação em um estado de erro quando há uma busca em um capítulo

* Zendesk #18053 - Aplicativo que usa o TVSDK falha em Marshmallow

O TVSDK travava no Android M OS quando a biblioteca TVSDK usa um código de néon que faz conversão YUV -> RGB de cores. Esse problema foi resolvido atualizando as funções que estão causando esse problema usando uma versão de código que não é de néon.

* Zendesk #18072 - Android M - Falha no aplicativo

Essa falha ocorre ao chamar as APIs MediaCodecList e MediaCodecInfo ao verificar se o perfil e o nível são compatíveis. A Adobe está buscando o suporte da Google para obter insights adicionais. Esse problema foi resolvido fornecendo uma solução temporária, carregando todas as informações do codec antecipadamente para evitar a chamada dessas APIs somente quando as informações do codec forem necessárias.

* Zendesk #18074 - Legendas em árabe que não funcionam no Nexus com Android 6.0

Esse problema foi resolvido fornecendo suporte ao mapa de fontes CTS do Android.

**Versão 1.4.15** (1.4.15.512) para iOS 6.0+

**Nota**: o módulo Nielsen foi removido da build do TVSDK, mas o TVSDK será atualizado em breve com um novo módulo de integração Nielsen.

* (ZD #2228) - Erro retornado da busca do manifesto indisponível em MediaPlayerNotification

Adição de metadados para expor conteúdo quando a notificação M3U8_PARSER_ERROR ocorre.

* (ZD #4437) - Falhas dentro do SDK do Adobe Primetime

Correção de uma falha relatada ao preparar legendas/áudio alternativo.

* (ZD #4487) - Rastreamento do canal linear de conteúdo

Reinicialização permitida do rastreador de heartbeat de vídeo durante uma sessão de reprodução de fluxo linear.

**Versão 1.4.14** (1.4.14.498) para iOS 6.0+

* (ZD #17260) - Falha em playlistManagerForURL

Correção de uma falha intermitente devido a problemas de simultaneidade.

**Versão 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` macro não preenchida

   * O código de erro 400 será exposto se o anúncio em linha tiver um criativo incorreto.
   * `[ERRORCODE]` A macro será codificada por URL.

* (ZD #3865) Integração do Heartbeat com anúncios do IMA

Correção de um erro em que a duração do vídeo era relatada incorretamente.

* Atualização do reprodutor de demonstração TVSDK para oferecer suporte ao iOS 9

Para oferecer suporte adequado ao iOS 9, é necessário configurar as exceções do Application Transportation Security. Para o propósito da demonstração, o ATS é completamente desativado.

**Versão 1.4.12** (1.4.12.464) para iOS 6.0+

* (ZD #4521) CRS Testando lado do cliente e SSAI

Corrigido o MD5 incorreto e reverso no URL 3P.

**Versão 1.4.12** (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI e CRS | Aprimorar: trate elementos dinâmicos em determinados URLs de arquivo de mídia.

Serviço de reempacotamento criativo atualizado para lidar adequadamente com anúncios com URLs criativos dinâmicos.

* (ZD #3654) Vazamento de memória na versão PSDK após 1.3.4.166

Correção de vazamento de memória no drmFramework com reprodução regular em dispositivos iOS 8.2

* (ZD #3988) O Preroll é ignorado ao buscar de volta após a primeira reprodução

Correção de um erro para que as políticas de anúncios pudessem ser desativadas corretamente.

* (ZD #4017) Solicitação à API do iOS para forçar a reprodução de um anúncio em uma busca retroativa

Resolvido com correção para ZD #4279

* (ZD #4279) Inserção de anúncio TVSDK do HLS - problema de redirecionamento 302 no iOS e na área de trabalho

Correção de um erro quando um ativo de anúncio usava um URL de redirecionamento relativo.

**Versão 1.4.9** (1.4.9.427) para iOS 6.0+

* (ZD #3075) Problema de acessibilidade da Internet - iOS

Adição de uma notificação para detectar quando a reprodução parou.

* (ZD #3193) Solicitação de uma API de alteração de perfil no TVSDK

Atualização de PTPlaybackInformation para expor a indicatedBitrate atualizada. Atualização da notificação BITRATE_CHANGE para ter mais tempo confiável e preciso para as taxas de bits relatadas do M3U8.

* (ZD #3324) Problemas de relatório de anúncios do Primetime quando nenhuma mídia de anúncio no VMAP

Suporte para ping de URLs vazios de rastreamento de ad break. O TVSDK agora verificará o início do ad break e concluirá os pings de ad breaks vazios

**Versão 1.4.8** (1.4.8.402)

* (ZD #3158) O IOS 7 falha em repetições completas de evento

**Versão 1.4.7** (1.4.7.382)

* (ZD #2197) Rastreamento de erros de anúncios. Adição de notificação para falha do ativo ao carregar manifesto.
* (ZD #2894) O Player faz quatro solicitações de manifesto de nível superior durante a reprodução.
* (ZD #2992) Auditude Relatando durações e identificadores estranhos.

**Versão 1.4.6**(1.4.6.325)

* (ZD #2197) Rastreamento de erros de anúncios. Adicionada notificação para falha do ativo ao carregar o manifesto

**Versão 1.4.5** (1.4.5.283)

* (ZD #2141) Implementação do Analytics para o aplicativo TreeHouse, adição da biblioteca AdobeAnalyticsPlugin.a para criar o pacote .
* Atualização da biblioteca de vídeo Heartbeats para 1.4.1.2
* (PTPALY-4226) (relacionado a ZD #2423) A execução da Redefinição de DRM pode resultar na exclusão dos dados do Documento de Aplicativo.

**Versão 1.4.4** (1.4.4.242)

* Atualização da Biblioteca de vídeo Heartbeats (VHL) para 1.4.1.

* (ZD #2435) Documentação do SDK da TV sobre atualizações de necessidades de análise

**Versão 1.4.2** (1.4.2.210 : iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOptions retornando vazio
* (ZD #2109) O Primetime PSDK 1.4.1.125 não funciona com o Xcode 5.1.1
* (ZD #2137) Falha no PSDK no iOS quando os metadados de DRM não podem ser carregados

**Versão 1.4.1** (1.4.1.125)

* (ZD #1107) Símbolos duplicados de CocoaLumberjack
* (ZD #1644) Modificar o Agente do usuário do iOS para direcionamento e relatórios
* (ZD #1850) Arquivos do Cocoa Lumberjack incluídos no SDK do iOS
* (ZD#1908) Tags personalizadas são ignoradas por PSDK se houver mais de 1

**Versão 1.4.0** (1.4.0.32)

* Zendesk #1024 - Recurso para remover anúncio de transmissão via manifesto

## Problemas conhecidos no 1.4 {#known-issues-in}

* No iOS TVSDK, todos os anúncios são compilados no manifesto de conteúdo. Comportamentos de anúncios são implementados pela busca com base na duração do conteúdo e dos segmentos de anúncios. Portanto, se as durações do segmento não forem precisas, a busca nem sempre pode terminar no quadro exato do início ou do fim do ad break. Mesmo que as durações estejam relacionadas ao quadro, há uma tolerância que a própria plataforma impõe na busca e pode haver alguns quadros, anúncios ou conteúdo exibidos. Essa é uma limitação da plataforma e a maneira como a inserção de anúncios funciona com o TVSDK no iOS.
* Nesse caso, a decisão de ignorar acontece no evento de busca. No entanto, como as durações do segmento de anúncio no manifesto não representam com precisão a duração real do anúncio, a busca não tem precisão de quadro. Portanto, você vê alguns quadros do anúncio quando as políticas do anúncio são aplicadas.
* RECORDING_ERROR: ocorreu um erro durante a gravação da tela.
* Pode ser que o vídeo de rotação de licença não seja reproduzido no iOS 11 e funcionará bem no iOS 9.x e no iOS 10.x.
* No suporte ao VPAID 2.0, se a reprodução estiver ativa no AirPlay, os anúncios VPAID serão ignorados.
* O drmNativeInterface.framework não vincula corretamente quando o target mínimo é definido como iOS7 (ou posterior).\
  Solução alternativa: especifique explicitamente a `libstdc++6`.  A biblioteca dylib da seguinte maneira: Vá para Target ->Criar fases->Vincular binário com bibliotecas e adicione `libstdc++.6.dylib`.

* O anúncio pós-implantação não é inserido para substituir a API.
* Buscar um ad break (sem sair dele) emite uma notificação de anúncio duplicado iniciar um ad break
* A definição currentTimeUpdateInterval não tem efeito.\
  Observação: em determinadas versões do iOS, o sistema operacional não carrega os recursos dentro do PSDKLibrary.framework automaticamente. É importante copiar manualmente o PSDKResources.bundle para os recursos do pacote do aplicativo: Vá para &quot;Criar fases&quot; e copie recursos do pacote.
* O aplicativo de referência não pode ser criado usando o Xcode 8 ou versões anteriores. iOS TVSDK versão 1.4.41 em diante, use o Xcode 9 para compilar.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
