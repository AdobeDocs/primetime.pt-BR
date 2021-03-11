---
title: Notas de versão do TVSDK 1.4 para iOS
description: Notas de versão do TVSDK 1.4 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK iOS 1.4
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '6550'
ht-degree: 0%

---


# Notas de versão do TVSDK 1.4 para iOS {#tvsdk-for-ios-release-notes}

As Notas de versão do TVSDK 1.4 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK iOS 1.4.

## Novos recursos {#new-features}

**Versão 1.4.45**

* Para estar em conformidade com o Xcode10, o TVSDK mudou de &quot;`libstdc++`&quot; para &quot;`libc++`&quot; e, como resultado, a versão mínima compatível é o iOS 7. Anteriormente, era o iOS 6.

**Versão 1.4.44**

* Nenhum novo recurso ou aprimoramentos nesta versão.

**Versão 1.4.43**

* Experiência semelhante à da TV de poder participar no meio de um anúncio sem acionar o rastreamento de anúncios parciais.\
   Exemplo: O usuário junta-se ao meio (em 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. Isso é de 10 segundos no segundo anúncio no intervalo.

   * O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido do terceiro anúncio.
   * Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente do terceiro anúncio são acionados.

* Adição da propriedade enableVodPreroll do tipo Booleano na interface PTAdMetadata . A propriedade pode ser usada para ativar o precedente em um fluxo de VoD. Se enableVodPreroll for NO, o PSDK não reproduzirá antes da exibição. Isso, no entanto, não tem impacto sobre os patins. O valor padrão de enableVodPreroll é YES.
* closedCaptionDisplayEnabled API da interface PTMediaPlayer está marcada como obsoleta do iOS v1.4.43 em diante. Para determinar se as legendas ocultas estão disponíveis para um determinado PTMediaPlayerItem, examine a propriedade subtitlesOptions de PTMediaPlayerMediaItem.

**Versão 1.4.42**

Nenhum recurso novo é adicionado nesta versão. Para obter uma lista de problemas corrigidos, consulte Problemas resolvidos.

**Versão 1.4.41**

Alterações na API:

* **isSecure**: Uma nova API é introduzida com o isSecure para proteger o reprodutor de gravar e gerar um erro. O valor padrão é true.
* **allowExternalRecording**: Uma nova API é introduzida para permitir o espelhamento de reprodução de ar para um conteúdo seguro. O espelhamento de reprodução de ar é tratado como gravação, portanto, o valor allowExternalRecording deve ser definido como &#39;True&#39;, para permitir o espelhamento de reprodução de ar ou definido como &#39;False&#39; para interromper o espelhamento de reprodução de ar para conteúdo seguro. Por padrão, o valor é true.

**Versão 1.4.40**

Nenhum recurso novo.

**Versão 1.4.39**

* O iOS TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.
* O TVSDK do iOS é atualizado para fazer solicitações de CRS do novo host do Akamai `primetime-a.akamaihd.net`.
* A nova configuração de nome de host fornece a entrega de ativos CRS por HTTP e HTTPS (SSL) em maior escala.

**Versão 1.4.36**

Integrar e certificar o VHL 2.0 no TVSDK do iOS : Reduza a barreira na implementação da VideoHeartbeatsLibrary diminuindo a complexidade das APIs.

**Versão 1.4.34**

* Informações de anúncio de rede

   As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. ID do anúncio, Sistema de anúncio e Extensões de anúncio VAST são fornecidas na classe `PTNetworkAdInfo` acessível por meio da propriedade `networkAdInfo` em um Ativo de anúncio. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como **Moat Analytics**.

**Versão 1.4.31**

* **** Métricas de faturamento Para acomodar os clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa, independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que o SDK gera um evento de início de fluxo, o reprodutor inicia periodicamente mensagens HTTP para enviar mensagens HTTP para o sistema de faturamento Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com o Adobe determina os valores reais.

* **Suporte a Várias CDN para** AdsTVSDK do CRS agora é compatível com Multi-CDN para anúncios CRS. Ao fornecer detalhes FTP para anúncios CRS, é possível especificar locais de CDN, diferentes do CDN Adobe padrão, como Akamai.

**Versão 1.4.29**

Na classe PTSDKConfig , a API forceHTTPS foi adicionada.

A classe PTSDKConfig fornece métodos para aplicar o SSL em solicitações feitas aos servidores de tomada de decisão de anúncio do Adobe Primetime, DRM e Video Analytics. Para obter mais informações, consulte os métodos `forceHTTPS` e `isForcingHTTPS` nesta classe. Se um manifesto for carregado por HTTPS, o TVSDK preservará o uso de conteúdo de HTTPS e respeitará esse uso ao carregar quaisquer URLs relativos desse manifesto.

**Observação**: As solicitações para domínios de terceiros, como pixels de rastreamento de anúncios, URLs de conteúdo e anúncios, e solicitações semelhantes não são modificadas, e é responsabilidade dos provedores de conteúdo e servidores de anúncios fornecer URLs compatíveis com HTTPS.

**Versão 1.4.18**

O Primetime iOS TVSDK agora é compatível com criações de Javascript VPAID 2.0 para permitir uma rica experiência interativa de anúncios em fluxo.

Para obter mais informações sobre o VPAID 2.0, consulte [VPAID ad support](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md).

**Versão 1.4.17**

* tvOS

   O TVSDK é compatível com aplicativos nativos do tvOS.
* Os seguintes tipos de conteúdo podem ser reproduzidos:

   * VOD
   * Ao vivo
   * AES-128
   * Áudio e legendas alternativas
   * FER

* Os seguintes tipos de anúncios podem ser exibidos:

   * Básico
   * VAST2
   * VAST3
   * VMA

* No momento, os seguintes recursos não são compatíveis:

   * Digital Rights Management (DRM)
   * Banners de anúncios
   * Linguagem de marcação de TV (TVML)

**Versão 1.4.13**

**Observação**: O módulo da Nielsen foi removido da build TVSDK, o TVSDK será atualizado em breve com um novo módulo de integração da Nielsen.

* **Fallback do anúncio, encadeamento de margarida na lógica de seleção do anúncio (Zendesk nº 3103)**

Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Ad fallback for VAST and VMAP ads](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md).

**Versão 1.4.9**

* **Sinalização de blecaute com substituição de conteúdo alternativo**

Como parte da atualização do TVSDK 1.4, agora também oferecemos suporte para acessar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos de manifesto em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

**Versão 1.4.8**

* **Biblioteca do Video Heartbeats (VHL) atualizada para a versão 1.5**

   * Capacidade de enviar metadados com início de vídeo e/ou início de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - Os heartbeats têm menos em média e menor tamanho

**Versão 1.4.7**

* **Suporte para individualização no local**

Suporte para instalações no local do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para ir para um terminal diferente.

* **Proteção de saída baseada em resolução**

As Políticas de DRM agora podem especificar a resolução mais alta permitida, dependendo dos recursos de Proteção de Saída do dispositivo. Por exemplo, &quot;Se o HDCP estiver disponível, permita que o conteúdo de resolução de até 1080p seja reproduzido e, se o HDCP não estiver disponível, permita que o conteúdo de resolução de até 480p seja reproduzido&quot;.

**Versão 1.4.4**

* **Atualização da Biblioteca do Video Heartbeats (VHL) para a versão 1.4.1.1**

   * Adicionada a capacidade de agrupar diferentes casos de uso de análises, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete . O ad break é inferido das chamadas de método trackAdStart e trackAdComplete .
   * A propriedade do indicador de reprodução não é mais necessária ao rastrear anúncios.
   * Adição de suporte para a ID de visitante do Marketing Cloud.

* **Integração de SDK da Nielsen**

   * O TVSDK agora é compatível com o envio de mTVR e MDPR ID3 beacons para o SDK da Nielsen sem qualquer integração personalizada. Para começar, baixe o SDK do aplicativo Nielsen para iOS 3.1.2.19.

**Versão 1.4.0**

* **Sinalização de blecaute com substituição de conteúdo alternativo**

   * Como parte da atualização do TVSDK 1.4, o TVSDK também agora oferece suporte para acessar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos de manifesto em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remover/substituir anúncios C3**

   * Agora, nenhum trabalho de preparação adicional é necessário para inserir dinamicamente novos anúncios nos ativos de VOD (video-on-demand) que estão saindo da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova funcionalidade poderosa também é útil nos casos em que o conteúdo ao vivo/linear é transmitido durante a transmissão e é imediatamente suspenso para uso como conteúdo sob demanda, sem tempo adequado para &quot;limpar&quot; o ativo.

## Certificação e suporte do dispositivo no 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Os seguintes recursos são **não** compatíveis com o TVSDK:
>
>* Movimentação lenta em qualquer plataforma ou versão.
>* Brincadeira ao vivo.


**Versão 1.4.43**

* O TVSDK 1.4.43 é certificado para iOS 11.

**Versão 1.4.29**

* O TVSDK 1.4.29 foi certificado para iOS 10.

**Versão 1.4.28**

* O TVSDK 1.4.28 foi certificado para iOS 10 Beta 7.
* Suporte a DRM para forçar HTTPS adicionando forceHTTPS e isForcingHTTPS APIs.
* Atualização das bibliotecas do VHL para 1.5.8, das bibliotecas do Adobe Mobile para 4.8.4 e da biblioteca do utilitário logger para o destino de implantação da versão 7.0.

**Versão 1.4.19**

Esta versão do TVSDK foi certificada com o FairPlay Support for iOS e tvOS.

**Versão 1.4.17**

* tvOS

   Esta versão do TVSDK inclui suporte para tvOS e foi certificada para fluxos HLS não criptografados.

   **Observação**: Lembre-se das seguintes diretrizes de compilação:

   * O suporte TVSDK tvOs é limitado a fluxos criptografados por não Adobe DRM. Você deve remover a referência a drmNativeInterface.framework nas configurações de build do tvOS. Os fluxos criptografados AES ainda são compatíveis.
   * A Apple requer que todos os aplicativos Apple TV estejam habilitados para código de bits, portanto, você deve ativar esse sinalizador nas configurações do projeto.

## Problemas resolvidos em 1.4 {#resolved-issues-in}

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

* Tíquete #36294 - iOS TVSDK não funciona com Xcode 10

   * Correção de problemas de compilação com TVSDK no XCode 10. Devido aos requisitos do XCode 10, os aplicativos criados no TVSDK para iOS 1.4.45 em diante exigem o direcionamento mínimo da implantação como iOS 7.0

* Tíquete #36321 - Discrepância observada no intervalo pesquisável entre PTMediaPlayer e a instância AVPlayer no estado &quot;Reproduzindo&quot;.
* Tíquete #36493 - `libstdc++` suporte no iOS 12

   * Correção de problemas de compilação com TVSDK no iOS 12. Os aplicativos criados em TVSDK para iOS 1.4.45 em diante exigem o direcionamento mínimo da implantação como iOS 7.0

**Versão 1.4.44**

* Tíquete Nº 34683 - O Tempo De Andamento Da Reprodução Do Anúncio Está Sendo Negativo

   * Verificações adicionais feitas para lidar com o caso em que há uma incompatibilidade entre a duração relatada pelo servidor de anúncios e o conteúdo real do anúncio.

* Tíquete #34801 - currentTime e localTime não eram atualizadas ao buscar uma nova posição durante o status pausado

   * A hora atual do player pode ser definida como zero caso o player esteja no estado pausado; anteriormente, o tempo atual era definido como zero somente no estado de reprodução.

* Tíquete #35037 - A reprodução é paralisada com URL incorreto ao retornar da inserção de anúncio com base em sinal.

   * Correção aprimorada fornecida para o problema fechado nº 34385 na versão 1.4.42. Adicionado isCancelled check and exception handling code para tornar a fila de operações mais robusta.

**Versão 1.4.43**

* (ZD#32990) - iOS: Reprodução de conteúdo em vez de anúncios em alguns pontos de sinalização. A API &#39;seletedMediaOptionInMediaSelectionGroup&#39; que fazia parte da interface AVPlayerItem agora foi movida para AVMediaSelection no iOS 11. O problema foi resolvido usando essa nova API.
* (ZD#33683) TVSDK removido == sufixo das cadeias de caracteres de metadados. O problema é corrigido na lógica de análise.
* (ZD#33905) - TVSDK do iOS fazendo chamadas para os arquivos de manifesto com dois agentes do usuário. O problema do agente do usuário foi corrigido na primeira chamada m3u8 (caso de instalação nova). Os M3u8 têm os mesmos agentes de usuário para todas as chamadas agora.
* (ZD#34293) - Os pré-rolls inseridos em fluxos LINEARES não são reproduzidos corretamente no iOS11. O problema é corrigido para anúncios pré-implantados.
* (ZD#34684) - Quando a política de ignorar o anúncio é aplicada, os quadros de anúncio precedentes são exibidos por alguns segundos. Uma nova API, enableVodPreroll, foi introduzida para desativar a reprodução de pré-visualização na reprodução do vod. O valor padrão para essa API é &quot;Sim&quot;. A API garante a omissão da compilação do conteúdo do anúncio no conteúdo principal.
* (ZD#34765) - Após chamar stop(), poucos segmentos de Transmissão ainda são baixados. Aprimoramento da API Stop() para evitar o download dos segmentos extras.
* (ZD#34865) - Os anúncios precedentes para livestream são truncados no iOS. Relacionado ao iOS11, e adicionar uma verificação adicional para confirmar se o fluxo é precedente ou conteúdo principal, trata desse problema.
* (ZD#35093) - Corrigido um cenário de failover em que, se a variante primária do fluxo falhar na inicialização (retorna 404), a reprodução não alterará para o fluxo de backup.

**Versão 1.4.42 (1.4.42.118)**

* (ZD#34385) - A reprodução é paralisada com um URL incorreto ao retornar da inserção de anúncios com base em sinal.

   Aumente as contagens simultâneas máximas para CustomAVAssetLoaderOperations, para que as leituras de manifesto possam continuar a ser executadas.
* (ZD#34373) - Os usuários finais não podem fazer stream para dispositivos conectados por HDMI, quando a gravação de fluxo é proibida.
* (ZD#32678) - O TVSDK não coleta as IDs de anúncio corretas no iOS.

   A ID do anúncio final do anúncio final agora é selecionada nos pings VHL, no caso de redirecionamentos VAST/VMAP.
* (ZD#33904) - O TVSDK não está registrado para notificações de AVFFoundation AVAudioSessionMediaServiceswereLostNotification e AVAudioSessionMediaServiceswereResetNotification.

   PTMediaServicesDidLostNotification e PTMediaServiceswereResetNotification agora podem ser registradas no aplicativo do reprodutor para obter as notificações quando os serviços de mídia são redefinidos ou perdidos.

* (ZD#33815) - Os clientes não podem atualizar suas regras de priorização e normalização do CRS sem precisar de uma atualização do aplicativo.

   Adicionadas getCRSRulesJsonURL e setCRSRulesJsonURL APIs ao TVSDK do iOS .

**Versão 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemas ao criar o aplicativo de referência com o TVSDK versão 1.4.41

   A partir desta versão, o Xcode 9 é necessário para compilar TVSDK para iOS.
* (ZD #29456) - A reprodução de ar começa no estado pausado

   Correção do problema de pausa que ocorre quando o vídeo é pausado ao entrar na reprodução de ar.
* (ZD #30371) - O horário de início do AdBreak muda ao inserirmos mais de 2 anúncios em fluxo linear

   Correção do erro ao tentar reproduzir conteúdo na Apple TV, o que impede a reprodução completamente
* (ZD #32146) - Nenhum PTMediaPlayerStatusError é recebido para o conteúdo do HLS Live no bloqueio do beta de desenvolvimento do iOS 11

   Nenhum PTMediaPlayerStatusError é recebido para conteúdo HLS Live e VOD no bloqueio usando Charles (conexão de soltar e 403)
* (ZD #29242) - A reprodução de vídeo do Airplay falha com anúncios ativados

   Quando os anúncios são ativados e o AirPlay é ativado, iniciando a reprodução de um vídeo, a reprodução do vídeo nunca é iniciada e nenhum erro é exibido
* (ZD#33341) - Os acionadores DRMInterface.h criam avisos no Xcode 9

   Correção de dois protótipos de bloco no DRMInterface.h, que estavam sem a palavra &quot;void&quot; nas listas de parâmetros
* (ZD#31979) - Não compila/executa quando é iOS 10 ou posterior para iPhone 7/iPhone7+

   Corrigida a Compilação de documentos IB para versões anteriores ao iOS 7 não é mais suportada
* (ZD#32920) - Tela em branco em uma quebra de anúncio e sem conclusão de quebra de anúncio

   Quando um Ad break está apresentando instâncias de anúncio e após a conclusão de uma instância de anúncio, uma tela em branco é exibida
* (ZD#32509) - Desativar a gravação de tela do iOS 11 Desativar a gravação de tela no iOS 11

* (ZD#33179) - Falha intermitente de evento no iOS11

   Correção da falha de evento no iOS 11

**Versão 1.4.40**  (1.4.40.72)

* (ZD #32465) - O reprodutor não pode manipular listas de reprodução mescladas.

   Chame completeLoadingWithError(com: Erro) para o alicerce AV tentar fluxos/ativação pós-falha alternativos.

* (ZD #31951) - Erro de TVSDK durante rotações de licença.

   Correção do problema de rotação de licença.
* (ZD #31951) - Tela em branco em uma quebra de anúncio e sem conclusão de quebra de anúncio.

   Solucionado o problema que fazia com que os anúncios VPAID do Facebook retornassem com frequência vários blocos CDATA em um único \&amp;lt;AdParameters\&amp;gt; nó VAST.
* (ZD #33336) - [iOS] TVSDK - Os pods de anúncio não estão sendo preenchidos, apesar de terem anúncios suficientes retornados pelo Freewheel.

   Relação pai-filho criada entre sequência e anúncio de fallback e classificação com base na sequência principal e no índice.

**Versão 1.4.39**  (1.4.39.43)

* (ZD #32178) - A versão do TVSDK do iOS está incorreta.

   A saída da versão TVSDK nos arquivos de log foi 1.0.211. Ela foi corrigida para exibir a versão correta.

* (ZD #32199) - Carregamento de anúncio ocioso - O vídeo não é exibido para o conteúdo.

   A linha do tempo local do Adbreak que não estava sendo inicializada anteriormente agora é atualizada antes do uso.

* (ZD #27528) - Vídeo, áudio ou ambos congelam de 1 a 45 segundos após a reprodução de um ativo, se o áudio secundário estiver definido como não padrão no iOS 1.2.

   Prepare e informe as faixas de áudio no estado Pronto.

* (ZD #30411) - Você pode obter resultados inesperados, como sem áudio ou áudio incorreto, se escolher um idioma secundário do Sap.

   Prepare e informe as faixas de áudio no estado Pronto.

* (ZD #32199) - Carregamento de anúncio ocioso - O vídeo não é exibido para o conteúdo.

   A linha do tempo local do Adbreak que não estava sendo inicializada anteriormente agora é atualizada antes do uso.

* (ZD #27528) - Vídeo, áudio ou ambos congelam de 1 a 45 segundos após a reprodução de um ativo, se o áudio secundário estiver definido como não padrão no iOS 1.2.

   Prepare e informe as faixas de áudio no estado Pronto.

* (ZD #30411) - Você pode obter resultados inesperados, como sem áudio ou áudio incorreto, se escolher um idioma secundário do Sap.

   Prepare e informe as faixas de áudio no estado Pronto.

**Versão 1.4.38**  (1.4.38.860)

* (ZD #29281) - iOS: Adicionar AdSystem e Creative Id a solicitações CRS

Uso da ID criativa e do AdSystem na solicitação do CRS com base nas regras de normalização do CRS

* (ZD #29176) - Falha em PTAdPolicyDeligate satAdBreakAsWatched:position

Falha devido ao AdBreak vazio é manipulado agora.

* (ZD #30125) - Anúncios programáticos não estão funcionando na plataforma iOS

Adição de suporte a anúncios programáticos no iOS.

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME Notification

O evento de metadados cronometrados não é disparado para a tag # EXT-X-PROGRAM-DATE-TIME com fluxos DRM AO VIVO.

**Versão 1.4.37 (1.4.37.842)**

* (ZD #28950 ) - Problema de reprodução de VOD

Problema de reprodução quando a tag # EXT-X-PLAYLIST-TYPE no fluxo é definida como Evento em vez de VOD

* (ZD #29281) - iOS: Adicionar AdSystem e Creative Id a solicitações CRS

Uso da Creative Id e AdSystem na solicitação do CRS com base nas regras de normalização do CRS.

* (ZD #29462) - Anúncio do TremorHub no VOD do A&amp;E causando uma falha nos aplicativos do iOS

**Versão 1.4.36 (1.4.36.835)**

* (ZD #29418) - Os casos com duração 0 (#EXT-X-CUE-OUT:0.000) estão fazendo com que o TVSDK do iOS pare ou trave a reprodução.

O problema é corrigido e a reprodução é iniciada corretamente.

* (ZD #29462) - Anúncio no VOD causando uma falha no TVSDK do iOS .

O problema foi corrigido. O TVSDK do iOS está criando uma exceção (AUDNetworkAdInfo::initWithAdId) e não está lidando com ela. A exceção é devido a uma ID de anúncio vazia.

* (ZD #29281) - Adicionar AdSystem e Creative ID às solicitações do CRS.

Inclua AdSystem e CreativeId como novos parâmetros nas solicitações 1401 e 1403 (todos os outros parâmetros permanecem os mesmos).

**Versão 1.4.35**  (1.4.35.830)

* (ZD #27830) - Precisa determinar programaticamente a diferença entre legendas ocultas e legendas no iOS.

O TVSDK agora expõe os dois tipos que podem ser usados para filtrar o tipo de legenda necessário.

* (ZD #29160) - As dicas de anúncio EXT-X-CUE-OUT não são spliced corretamente no TVSDK iOS.

Com EXT-X-CUE-OUT, o anúncio intermediário está sendo reproduzido agora.

* (ZD #29100) - O aplicativo falha quando o usuário é depurado até o fim de um filme.

Correção de várias falhas relacionadas à sincronização.

* (ZD #28785), (ZD #27712) e (ZD #25076) - O aplicativo iOS está travando durante os grandes eventos ao vivo.

Correção de várias falhas relacionadas à sincronização.

**Versão 1.4.34**  (1.4.34.815 para iOS 6.0+)

* (ZD# 28481) - FFERE a interrupção devido à chave incorreta estar anexada ao final de um ad break para esses fluxos FER

Para um fluxo FER, a chave antes do ad break é inserida após o fim do ad break. Esse problema foi resolvido ao anexar a *última chave vista* no final do ad break.

**Versão 1.4.33**  (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Ativar CRS para subcontas

Habilitado ao enviar o URL criativo original para a solicitação CRS 1401 em vez do URL normalizado, de acordo com o requisito para o back-end do CRS.

* (ZD# 26218) - Problema de carregamento de PSDKResources.bundle

Esse problema foi resolvido atualizando o carregamento de recursos para procurar de todos os pacotes disponíveis.

* (ZD# 27460) Primeira chamada de anúncio intermediário - POST para cdn.auditude<span></span>.com retornando 403.

A nova conta CDN não pode lidar com uma solicitação de CDN de POST. Esse problema foi resolvido atualizando o código para fazer com que a solicitação de anúncio `cdn.auditude.com` fosse GET em vez de POST.

**Versão 1.4.32**  (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Suporte para valores decimais para quebras de anúncios VMAP.

Quando o conteúdo não era segmentado ao longo das quebras de anúncios definidas, os números inteiros causavam inserções inesperadas de anúncios. O problema foi resolvido ao não converter os valores decimais em números inteiros.

* (ZD# 27189) O conteúdo AES com a tag EXT-X-DISCONTINUITY-SEQUENCE não está sendo reproduzido corretamente.

O problema foi resolvido colocando a tag no início da lista de reprodução.

**Versão 1.4.31**  (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar métricas de uso do TVSDK para faturamento

Para obter mais informações, consulte [Métricas de Faturamento](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md).

* (ZD# 24642) Suporte Picture-in-Picture para TVSDK

O recurso picture-in-picture, que em alguns casos não funcionava corretamente, foi corrigido.

* (ZD# 25246) Sinais de ad break incorretos

Esse problema foi resolvido alinhando tags de descontinuidade em manifestos de variante.

* (ZD# 26218) O processo de compilação do aplicativo é complicado ao tentar incluir PSDKLibrary.framework na estrutura do aplicativo do cliente

Esse problema foi resolvido com o empacotamento do PSDKLibrary.framework, conforme solicitado.

* (ZD# 26364) Suporte a vários CDN para anúncios CRS

<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Atraso na reprodução de alguns fluxos no iOS 10.

Esse problema foi resolvido fornecendo uma solução alternativa para fluxos que não têm uma extensão M3U8.

**Versão 1.4.30**  (1.4.30.754 para iOS 6.0+)

Os seguintes problemas foram resolvidos para TVSDK nesta versão:

* (ZD# 24180) Adicionar um cabeçalho personalizado ao lista de permissões

Um novo cabeçalho personalizado foi adicionado à lista de permissões TVSDK.

* (ZD# 25016) O fluxo de failover é selecionado aleatoriamente quando os parâmetros de controle ABR são definidos

Esse problema foi resolvido mantendo os fluxos ABR em ordem quando as configurações ABR são fornecidas com a configuração inicialBitrate em um fluxo que inclui URLs de failover. Isso evitará reproduzir os fluxos de failover em vez do primário.

* (ZD# 25076) Falha em PTAuditudeAdResolver loadComplete

O problema em que uma falha ocorria durante o início/parada rápido de várias instâncias de PTMediaPlayer com anúncios foi corrigido.

* (ZD# 25960) Nenhuma tara adicional subscrita acionando a transmissão de notificação de alteração de metadados

O problema em que uma tag subscrita não é notificada quando aparece antes do primeiro segmento no manifesto foi corrigido.

* (ZD# 26084) PSDK acionando um 106000.101000.O decodificador -11833 não encontrou erro ao fazer a transição do último ad break para o conteúdo do entretenimento

Quando o último horário de início do ad break do VMAP cair antes da duração total ser concluída, em determinadas condições, a chave não será inserida até o final do último ad break. Esse problema foi corrigido.

* A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

   * (ZD #22351) VHL - Analytics: Duração do ativo de vídeo ao vivo

Esse problema foi resolvido adicionando a API assetDuration a `PTVideoAnalyticsTrackingMetadata` para atualizar a duração do ativo para fluxos Live/Lineares e fornecer uma lógica para verificar o fluxo ao vivo.

* (ZD# 22675) VHL - Analytics: Atualização da duração do ativo de vídeo ao vivo

Esse problema é igual ao ZD nº 22351.

* (ZD #25908) VHL - Analytics: Falha no evento do Adobe Heartbeat

Esse problema foi resolvido com a atualização da implementação para usar a versão mais recente do VHL para iOS versão 1.5.9 para melhorar a estabilidade e o desempenho.

* (ZD #25956) VHL - Analytics: Falha ao reproduzir vídeos repetidamente

Esse problema é o mesmo que ZD #25908.

**Versão 1.4.29**  (1.4.29.743)

* (ZD# 23901) Anúncios de terceiros não estão sendo reproduzidos

Esse problema foi resolvido movendo-se para a estrutura de URL CRS v3 para incluir a ID da zona no URL reempacotado.

* (ZD #25183) Problemas com a reprodução de DRM no tvOS e iOS

Esse problema foi resolvido fornecendo suporte para várias tags principais necessárias para o suporte a vários DRM.

* (ZD# 25334) O TVSDK não reproduz um conteúdo compartilhado do cDVR

Esse problema foi resolvido impedindo o TVSDK de converter cadeias de caracteres vazias em URLs absolutos.

* (ZD# 25347) Definir cabeçalho HTTP personalizado em AVURLAsset

Foi adicionado suporte para cabeçalhos personalizados em solicitações de segmento por meio da classe PTNetworkConfiguration.

**Versão 1.4.28**  (1.4.28.722)

* (ZD #24549) Várias chamadas de rastreamento de anúncio

Esse problema foi resolvido com a atualização do gerenciador de linha do tempo para acompanhar as notificações em um objeto específico quando vários reprodutores são criados.

* (ZD #24758) PTManifestLogger não é compatível com iOS 8

Esse problema foi resolvido atualizando a biblioteca do utilitário logger para o destino de implantação da versão 7.0.

* (ZD #24775) Fluxo atrasado devido a anúncios

Esse problema foi resolvido calculando corretamente o desvio da duração nas listas de reprodução do evento.

* (ZD #24799) Alguns dos episódios não estão sendo reproduzidos no iOS APP

Esse problema foi resolvido usando o servidor da Web local para legendas quando os arquivos WebVTT são geo-restritos.

**Versão 1.4.27**  (1.4.27.711) para iOS 6.0+

* (ZD #24089) - Otimizações para a resolução de anúncios em longos fluxos DVR

Esse problema foi resolvido adicionando várias otimizações para reduzir o tempo necessário para processar a janela do DVR em fluxos ao vivo/lineares.

* (ZD #21554) - Beacons de erro TVSDK não acionados para tipo de aplicativo = video/mp4

Esse problema foi resolvido com a habilitação do reprodutor para fazer o ping dos URLs de rastreamento de erros corretos em formatos de ativos inválidos.

* (ZD #24424) - Falha do tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS tem origem dentro do PSDKLib para iOS em dispositivos de hardware mais recentes.

A falha que ocorria devido a uma instância do reprodutor de mídia desalocada, quando a reprodução é alternada rapidamente entre fluxos diferentes, foi corrigida.

* (ZD #24575) - Falha no TVSDK em dispositivos de 32 bits quando enableDebugLog=true

O problema no formato de log que causou a falha em dispositivos de 32 bits quando o registro está ativado foi corrigido.

**Versão 1.4.26**  (1.4.26.702) para iOS 6.0+

* (ZD# 20213) - O TVSDK FW precisa ser dinâmico/modularizado para XCode7

   * Corrigido ao atualizar as bibliotecas com suporte ao módulo

**Versão 1.4.25**  (1.4.25.684) para iOS 6.0+

* (ZD #19629) - Vídeo em tempo real é pausado ao entrar no Airplay para ATV 4

Esse problema foi resolvido adicionando um período de espera após a remoção de itens antigos, mas antes de adicionar novos itens ao AVQueuePlayer. Sem o período de espera, as notificações são enviadas para o item incorreto.

* (ZD #19856) - Nenhuma legenda é exibida quando habilitada por padrão

Os problemas na lista de reprodução do webvtt, que fazia com que as legendas não fossem exibidas corretamente, foram corrigidos.

* (ZD #21590) - Desempenho de vídeo e rastreamento nas criações de origem mais recentes

O problema sobre a duração do vídeo ausente no VideoAnalytics foi corrigido.

* (ZD #20202) - A configuração de estilo de legendas personalizadas trava o aplicativo iOS

Esse problema foi resolvido adicionando verificações de objeto nulo adicionais ao configurar estilos de subtítulo.

* (ZD #20709) - duração do vídeo relatada como 0 no rastreamento de início do vídeo

Esse problema é o mesmo que (ZD #21590).

* (ZD #22280) - A Duração de vídeo do Analytics está sendo definida como 0

Esse problema é o mesmo que (ZD #21590).

* (ZD #22592) - Problemas com o Airplay no Primetime

Esse problema é o mesmo de (ZD #19629).

* (ZD#22922) - Mudança manual da taxa de bits para iOS

Esse problema foi resolvido fornecendo uma opção para especificar a taxa de bits máxima.

* (ZD #23084) - Conformidade da Apple para redes somente IPv6

Os símbolos que não foram recomendados pela Apple para compatibilidade IPv6 foram removidos.

**Versão 1.4.24**  (1.4.24.661) para iOS 6.0+

* ZD #2548) - Suporte do Primetime para publicidade interativa em dispositivos móveis - VPAID 2.0

Esse problema foi resolvido atualizando a lógica para mostrar a visualização do reprodutor se um anúncio VPAID não for reproduzido.

* (ZD #20101) - A implementação do Capítulo personalizado aciona o evento de início do capítulo durante a reprodução do anúncio

Esse problema foi resolvido atualizando o VideoAnalyticsTracker para detectar apropriadamente o início/a conclusão do capítulo durante a transição entre os limites de capítulo e não capítulos.

* (ZD #20784) - Analytics: Acionamento de conclusões de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido adicionando uma lógica para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo.

As seguintes bibliotecas foram atualizadas:

* Biblioteca AdobeMobile para 4.10.0
* Biblioteca do VHL para 1.5.6
* Biblioteca VHL-Nielsen para 1.6.7
* (ZD #21855) - As legendas não são reproduzidas após a exibição

Nesta edição, tags de descontinuidade duplicadas faziam com que as legendas não fossem exibidas após a exibição. Esse problema foi resolvido com a remoção das tags de descontinuidade próximas umas das outras.

* (ZD #21994) - Cadeia de caracteres fora dos limites em PTHLSUtils

A causa mais provável da falha é quando um EXT-X-KEY tem um URL que está entre aspas.

* ZD #22074) - Falha do AUDVAST ocorrendo uma vez por minuto no iOS

Na versão 1.4.23, a falha causada pela presença de caracteres não seguros em um URL de redirecionamento VAST foi corrigida. No entanto, o TVSDK continuava ignorando esses anúncios.

Esse problema foi resolvido com o uso de caracteres não seguros e a permissão de reprodução dos anúncios.

* (ZD #22694) - PTMediaPlayer.  Exibir está oculto pelo reprodutor

Esse problema foi resolvido atualizando a lógica para mostrar a visualização do reprodutor se um anúncio VPAID não for reproduzido.

**Versão 1.4.23**  (1.4.23.641) para iOS 6.0+

* (ZD #18016) - Nenhuma resposta do SDK do Primetime com uma condição de rede incorreta

Esse problema foi resolvido melhorando a notificação de erro quando ocorre um erro fatal da AVFFoundation e para permitir que o aplicativo gerencie a reinicialização após o erro.

* (ZD #20580) - Falha no PTSplicerManager

Esse problema foi resolvido fornecendo proteção adicional contra problemas de simultaneidade que causam a falha.

* (ZD #21782) - Código de erro do iOS 10100

O problema em que o TVSDK retornava um erro 101000 ao iniciar a reprodução em fluxos de DRM de acesso ao Adobe foi corrigido.

* (ZD #21889) - A reprodução de anúncios online e conteúdo offline falha

O problema em que a reprodução falhava após a correção de um anúncio no conteúdo offline criptografado AES.

* (ZD #22074) - Falha do AUDVAST ocorrendo uma vez por minuto no iOS

Esse problema foi resolvido melhorando o tratamento de tags de anúncios VAST de terceiros que têm caracteres inválidos no URL.

* (ZD #22257) - O TVSDK falha ao reproduzir o fluxo de DRM

O problema em que o TVSDK que retornava um erro 101000 ao iniciar a reprodução em fluxos de DRM de acesso ao Adobe foi corrigido.

**Versão 1.4.22**  (1.4.22.627) para iOS 6.0+

* (ZD #18709) - Falha no TVSDK para iOS

O problema sobre uma falha que ocorria em alguns fluxos protegidos por DRM de Adobe Access foi corrigido.

* (ZD #18850) - Atualizar lógica de seleção criativa com base nas regras do CRS

Esse problema foi resolvido adicionando um arquivo de configuração .json para especificar a prioridade da seleção criativa.

* (ZD #19770) - O feed de vídeo AES protegido não está mais sendo reproduzido

O problema em que certos fluxos redirecionados 302 estavam falhando na reprodução foi corrigido.

* (ZD #19629) - Vídeo em tempo real é pausado ao entrar no Airplay para ATV 4

Esse problema foi resolvido adicionando uma solução alternativa para a pausa de vídeo ao vivo quando a reprodução de ar está ativada para dispositivos Apple TV 4. O problema parece ser um problema da Apple TV 4.

* (ZD #21119) - O TVSDK é paralisado após a reprodução do anúncio

Foi adicionado suporte para fluxos criptografados AES com uma sequência IV ao usar a inserção do anúncio.

* (ZD #21125) - Retorno de pausa de anúncio ao vivo/linear antecipadamente

Foi adicionado suporte para retornar de um ad break antes da reprodução até a conclusão do ad break. O retorno antecipado é indicado por meio de uma tag de manifesto personalizada.

* (ZD #21224) - Suporte Airplay para fluxos tokens do Akamai

As APIs foram adicionadas à classe PTNetworkConfiguration para anexar cookies como parâmetros de URL nos segmentos para determinados fluxos tokens do Akamai.

* (ZD #21287) - Log irrelevante

Correção de um problema com algumas instruções de log exibidas por padrão no console do xcode, mesmo quando o registro está desativado.

* (ZD #21446) - Eventos de ad break às vezes não acionados pelo TVSDK

Em fluxos de EVENTO, as quebras de anúncio não são acionadas corretamente na build da versão anterior. Essa build aborda esse problema.

**1.4.21**  (1.4.21.605) para iOS 6.0+

* (ZD #20749) - O fallback ignora respostas VAST não vazias; Os URLs de rastreamento de anúncios adicionais são acionados

Um problema com pings duplicados em anúncios de fallback foi resolvido.

**1.4.20**  (1.4.20.590) para iOS 6.0+

* (ZD #18639) - O TVSDK está usando CPU/recursos excessivos em um ativo de gravação a quente longo prazo

O uso excessivo de CPU/recursos foi corrigido nos dois níveis. Primeiro, permitindo que a função de atualização de tempo seja executada em uma fila global, em vez do thread principal, e otimizando o uso da CPU para analisar o manifesto com o m3u8 processado e armazenado em cache anteriormente.

* (ZD #19349) - Os anúncios precedentes estão sendo ignorados ao diminuir a conexão de rede.

Esse problema foi resolvido fornecendo um evento de tempo limite (requestTimeout) ao aplicativo e aos adMetadata .  adRequestTimeout API para substituir o tempo limite padrão de 10 segundos.

* (ZD #19446) - Notificação ausente em fluxos ao vivo

Esse problema foi resolvido permitindo que o aplicativo assinasse EXT-X-PROGRAM-DATE-TIME em fluxos ao vivo.

* (ZD #19459) - Falha ao preparar áudio alternativo com PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Falha - [PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]

Esse problema é o mesmo do Zendesk nº 19459.

* (ZD #19574) - O TVSDK não está retornando dados de resposta M3U8 para conteúdo de DRM ou não-DRM

No carregamento inicial do arquivo de manifesto em PTMediaPlayerItem.preparationToPlay, se o carregamento do manifesto falhar, o TVSDK não informa o corpo da resposta de falha ao aplicativo.

Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro para o aplicativo.

* (ZD #19615) - A lógica de fallback não está funcionando

Na implementação atual, os anúncios de fallback foram ignorados e não foram recompactados, a menos que esses anúncios estejam no formato m3u8. Esse problema foi resolvido adicionando também o suporte para reempacotar anúncios de fallback.

* (ZD #19770) - O TVSDK falha ao reproduzir qualquer conteúdo AES protegido com redirecionamento 302

O problema de redirecionamento foi corrigido, pois o URL de redirecionamento estava sendo apagado por cleanConnectionData antes de poder ser usado para analisar o manifesto.

* (ZD #19856) - As legendas não são exibidas para algumas taxas de bits quando ativadas por padrão

Esse problema foi resolvido com o tratamento do erro do iOS nos segmentos dos fluxos nos quais as legendas não são exibidas.

* (ZD #19868) - O TVSDK falha quando um anúncio inválido é acessado por tráfego

A falha no TVSDK que estava desalocando incorretamente uma instância do analisador vasto foi corrigida.

* (ZD #20180) - Anúncios VPAID são ignorados ocasionalmente

O tipo MIME JavaScript nem sempre estava sendo incluído ou considerado como um tipo MIME válido. Esse problema foi resolvido incluindo o JavaScript como um tipo MIME válido.

* (ZD #20749) - O fallback ignora respostas VAST não vazias; Os URLs de rastreamento de anúncios adicionais são acionados

Foi corrigido o problema em que alguns dos criativos não estão sendo reembalados.

**Versão 1.4.19**  (1.4.19.563) para iOS 6.0+

* ZD #18639) - O TVSDK usa CPU/recursos excessivos em um ativo de gravação a quente longo prazo

Esse problema foi resolvido otimizando a reescrita da lista de reprodução do DRM m3u8 em bits de cache da lista de reprodução que foram reescritos anteriormente. Isso é mais relevante quando você reproduz fluxos em tempo real do m3u8 para os quais o m3u8 é baixado após cada download de segmento.

* (ZD#18956) - player.drmManager é nulo quando o ponto de interrupção é definido no Player de demonstração do iOS

Esse problema foi resolvido com a atualização da implementação da API PTMediaPlayer.drmManager para coletar o DRMManager da estrutura DRM.

**Versão 1.4.18**  (1.4.18.557) para iOS 6.0+

* (ZD #18844) Rastreamento do indicador de reprodução para conteúdo ao vivo no player do iOS.

Esse problema foi resolvido permitindo que os aplicativos definissem seu próprio valor do indicador de reprodução.

* Zendesk #18518 - Se o nome do vídeo não for especificado, o nome do TVSDK assumirá como padrão *player baseado no PSDK.*

Esse problema foi resolvido com a remoção do valor padrão do nome do reprodutor.

**Versão 1.4.17**  (1.4.17.545) para iOS 6.0+

* Zendesk #2228 - Aprimore o TVSDK para retornar a resposta JSON da busca de um manifesto

Em vez de enviar um erro quando o conteúdo não é M3U8, a Estrutura de DRM retorna um DRMMetadata nulo. O problema foi resolvido adicionando metadados para expor o conteúdo quando ocorreu a notificação M3U8_PARSER_ERROR.

* Zendesk #2231 - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification

Mesma resolução do Zendesk nº 2228

* Zendesk #3304 - macro VAST 3.0 `[ERRORCODE]` não sendo preenchida

O problema em que o SDK do Auditude não envia um ping quando o URL de rastreamento tem espaços no início foi resolvido.

* Zendesk #17294 - Falha SecKeyRawSign

Uma possível falha quando o código do cliente usa a cadeia de chaves foi resolvida.

* Zendesk #18008 - Cookies de suporte para iOS8+ para suportar fluxos com tokens

Os fluxos tokens do Akamai exigem que os cookies sejam enviados em solicitações de segmento, e isso não foi possível no iOS 7 e anterior. A partir do iOS 8, a Apple adicionou uma API que permite que os cookies sejam transmitidos para solicitações de segmento. Esse suporte agora está disponível no TVSDK . Também foi adicionado suporte para enviar um agente-usuário, se disponível.

* Zendesk #18166 - TVSDK 1.4.15 fornece centenas de avisos ao compilar com DWARF com opções de arquivo dSYM

Todos os avisos foram resolvidos.

**Observação**: Bibliotecas compatíveis com tvOS foram adicionadas para TVSDK .

**Versão 1.4.16**  (1.4.16.1454)

* Zendesk # 3875 - Tab S Crashes durante a reprodução

Reverter a dependência de OKHTTP no auditude do CRS porque o TVSDK agora usa diretamente a httpurlconnection em vez de curl. O problema foi resolvido limpando exceções antes de fazer outra chamada JNI.

* Zendesk nº 4487 - Rastreamento do canal linear de conteúdo

O problema foi resolvido reinicializando o rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17919 - Android - A busca de conteúdo causa erro de pulsação

O problema era resolver o heartbeat em um estado de erro quando há uma busca em um capítulo

* Zendesk #18053 - Aplicativo que usa o TVSDK falha no Marshmallow

O TVSDK estava travando no Android M OS quando a biblioteca TVSDK usa um código neon que faz conversão de cores YUV -> RGB. Esse problema foi resolvido atualizando as funções que estão causando esse problema usando uma versão que não seja neon do código .

* Zendesk #18072 - Android M - Falha do aplicativo

Essa falha ocorre ao chamar as APIs MediaCodecList e MediaCodecInfo ao verificar se o perfil e o nível são compatíveis. O Adobe está buscando o suporte do Google para obter informações adicionais. Esse problema foi resolvido fornecendo uma solução temporária carregando todas as informações do codec antecipadamente para evitar chamar essas APIs somente quando as informações do codec forem necessárias.

* Zendesk #18074 - Legendas árabes que não funcionam no Nexus com Android 6.0

Esse problema foi resolvido fornecendo suporte para o mapa de fontes CTS do Android.

**Versão 1.4.15**  (1.4.15.512) para iOS 6.0+

**Observação**: O módulo da Nielsen foi removido da build TVSDK, mas o TVSDK será atualizado em breve com um novo módulo de integração da Nielsen.

* (ZD #2228) - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification

Adição de metadados para expor o conteúdo quando a notificação M3U8_PARSER_ERROR ocorre.

* (ZD #4437) - Falhas no SDK do Adobe Primetime

Correção de uma falha relatada ao preparar legendas/áudio alternativo.

* (ZD #4487) - Rastreamento de canal linear de conteúdo

Autorizada reinicialização do rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

**Versão 1.4.14**  (1.4.14.498) para iOS 6.0+

* (ZD #17260) - Falha em playlistManagerForURL

Correção de uma falha intermitente devido a problemas de simultaneidade.

**Versão 1.4.13**  (iOS 6.0+)

* (ZD #3304) - A macro VAST 3.0 `[ERRORCODE]` não está sendo preenchida

   * O código de erro 400 será exposto se estiver em linha   anúncio tem anúncios ruins.
   * `[ERRORCODE]` será codificada no URL.

* (ZD #3865) Integração de heartbeat com anúncios IMA

Correção de um erro em que a duração do vídeo era relatada incorretamente.

* Reprodutor de demonstração TVSDK atualizado para oferecer suporte ao iOS 9

Para oferecer suporte adequado ao iOS 9, é necessário configurar as exceções do Application Transportation Security. Para o objetivo da demonstração, o ATS é totalmente desativado.

**Versão 1.4.12**  (1.4.12.464) para iOS 6.0+

* (ZD nº 4521) Teste de CRS no lado do cliente e SSAI

Correção de MD5 reverso incorreto em URL 3P.

**Versão 1.4.12**  (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI e CRS | Reforçar: Manipule elementos dinâmicos em determinados URLs de arquivo de mídia.

Serviço de reempacotamento criativo atualizado para lidar corretamente com anúncios com URLs criativos dinâmicos.

* (ZD #3654) Vazamento de memória na versão PSDK após 1.3.4.166

Correção de vazamento de memória no drmFramework com reprodução regular em dispositivos iOS 8.2

* (ZD #3988) A pré-rolagem é ignorada ao buscar de volta nela após a primeira reprodução

Correção de um erro para que as políticas de anúncios pudessem ser desativadas corretamente.

* (ZD #4017) Solicitação da API do iOS para forçar a reprodução de anúncio em uma busca retroativa

Resolvido com correção para ZD nº 4279

* (ZD #4279) Inserção de anúncio TVSDK do HLS -302 problema de redirecionamento no iOS e no desktop

Correção de um erro quando um ativo de anúncio estava usando um URL de redirecionamento relativo

**Versão 1.4.9**  (1.4.9.427) para iOS 6.0+

* (ZD #3075) Problema de acessibilidade na Internet - iOS

Adição de uma notificação para detectar quando a reprodução parou.

* (ZD #3193) Solicitação de uma API de alteração de perfil no TVSDK

PTPlaybackInformation atualizado para expor a taxa de bits indicada atualizada. A notificação BITRATE_CHANGE foi atualizada para ser mais confiável em tempo e precisa para as taxas de bits relatadas pelo M3U8.

* (ZD #3324) Problema de relatório de anúncios do Primetime quando não há mídia de anúncio no VMAP

Suporte para ping de URLs de rastreamento de ad break vazias, o TVSDK agora verificará o início do ad break e concluirá pings para ad breaks vazios

**Versão 1.4.8**  (1.4.8.402)

* (ZD #3158) O IOS 7 falha em reproduções completas de eventos

**Versão 1.4.7**  (1.4.7.382)

* (ZD #2197) Rastreamento de erros de anúncios. Falha ao carregar o manifesto da notificação do ativo adicionada.
* (ZD #2894) O Player faz quatro solicitações de manifesto de nível superior durante a reprodução.
* (ZD #2992) Auditude Reportando durações e identificadores estranhos.

**Versão 1.4.6** (1.4.6.325)

* (ZD #2197) Rastreamento de erros de anúncios. A notificação adicionada para o ativo falhou ao carregar o manifesto

**Versão 1.4.5**  (1.4.5.283)

* (ZD #2141) A implementação do Analytics para o aplicativo TreeHouse adicionou a biblioteca AdobeAnalyticsPlugin.a para criar o pacote .
* Atualização da biblioteca do Video Heartbeats para 1.4.1.2
* (PTPALY-4226) (relacionado ao ZD #2423) A execução da redefinição de DRM pode resultar na exclusão dos dados do Documento do Aplicativo.

**Versão 1.4.4**  (1.4.4.242)

* Atualização da Biblioteca do Video Heartbeats (VHL) para 1.4.1.

* (ZD #2435) Documentação do SDK da TV sobre necessidades de análise

**Versão 1.4.2**  (1.4.2.210) : iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOptions retornando vazio
* (ZD #2109) O Primetime PSDK 1.4.1.125 não funciona com o Xcode 5.1.1
* (ZD #2137) Falha no PSDK no iOS quando os metadados de DRM não podem ser carregados

**Versão 1.4.1**  (1.4.1.125)

* (ZD #1107) Símbolos duplicados de cocoaLumberjack
* (ZD #1644) Modificar o agente de usuário do iOS para direcionamento e relatórios
* (ZD #1850) Arquivos Cocoa Lumberjack incluídos no SDK do iOS
* (ZD#1908) Tags personalizadas são ignoradas pelo PSDK se houver mais de 1

**Versão 1.4.0**  (1.4.0.32)

* Zendesk #1024 - Recurso para remover anúncio do fluxo por meio do manifesto

## Problemas conhecidos no 1.4 {#known-issues-in}

* No TVSDK do iOS , todos os anúncios são compilados no manifesto de conteúdo. Os comportamentos de publicidade são implementados pela busca com base na duração dos segmentos de conteúdo e anúncios. Portanto, se a duração do segmento não for precisa, a busca nem sempre pode terminar no quadro exato do início ou do fim do ad break. Mesmo que as durações estejam no quadro, há uma tolerância que a plataforma em si impõe à busca e pode haver alguns quadros, anúncios ou conteúdo exibidos. Essa é uma limitação da plataforma e a maneira como a inserção de anúncios funciona com TVSDK no iOS.
* A decisão de ignorar ocorre no evento de busca neste caso. No entanto, como a duração do segmento de anúncio no manifesto não representa com precisão a duração real do anúncio, a busca não é precisa do quadro. Assim, você vê alguns quadros do anúncio quando as políticas de anúncios são aplicadas.
* RECORDING_ERROR: Ocorreu um erro ao gravar a tela.
* Pode ser que o vídeo de Rotação de Licença não seja reproduzido no iOS 11 e será reproduzido no iOS 9.x e iOS 10.x.
* No suporte a VPAID 2.0, se a reprodução estiver ativa sobre o AirPlay, os anúncios VPAID serão ignorados.
* O drmNativeInterface.framework não é vinculado corretamente quando o destino mínimo é definido como iOS7 (ou posterior).\
   Solução alternativa: Especifique explicitamente o `libstdc++6`.  biblioteca de dilib da seguinte forma: Vá para Target->Criar fases->Link binário com bibliotecas e adicione `libstdc++.6.dylib`.

* Anúncio pós-rolagem não é inserido para substituir a API.
* A busca em um ad break (sem sair) emite uma duplicata e inicia uma notificação de ad break
* A definição de currentTimeUpdateInterval não tem efeito.\
   Observação: Em determinadas versões do iOS, o SO não carrega os recursos dentro do PSDKLibrary.framework automaticamente. É importante copiar manualmente o PSDKResources.bundle para os recursos de pacote do aplicativo: Vá para &quot;Criar fases&quot; e copie recursos do pacote.
* O Aplicativo de referência não pode ser criado usando o Xcode 8 ou versões inferiores. A partir da versão 1.4.41 do TVSDK do iOS, use o Xcode 9 para compilar.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .