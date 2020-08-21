---
title: Notas de versão do TVSDK 1.4 para iOS
seo-title: Notas de versão do TVSDK 1.4 para iOS
description: As Notas de versão do TVSDK 1.4 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK iOS 1.4
seo-description: As Notas de versão do TVSDK 1.4 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK iOS 1.4
uuid: c1df12bd-aa21-47e8-ade4-1e497882ce9b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 452f8699-7857-49ab-9caa-22204b19fe4a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '6578'
ht-degree: 0%

---


# Notas de versão do TVSDK 1.4 para iOS {#tvsdk-for-ios-release-notes}

As Notas de versão do TVSDK 1.4 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK iOS 1.4.

## Novos recursos {#new-features}

**Versão 1.4.45**

* Para estar em conformidade com o Xcode10, o TVSDK foi movido de &quot;`libstdc++`&quot; para &quot;`libc++`&quot; e, como resultado, a versão mínima compatível é o iOS 7. Antes era o iOS 6.

**Versão 1.4.44**

* Nenhum novo recurso ou aprimoramentos nesta versão.

**Versão 1.4.43**

* Experiência semelhante à da TV de poder participar do meio de um anúncio sem acionar o rastreamento parcial do anúncio.\
   Exemplo: O usuário ingressa no meio (em 40 segundos) de um intervalo de anúncios de 90 segundos que consiste em três anúncios de 30 segundos. Dez segundos depois do segundo anúncio no intervalo.

   * O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.
   * Os rastreadores de anúncios para o anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores apenas para o terceiro anúncio são acionados.

* Adicionada a propriedade enableVodPreroll do tipo Booliano na interface PTAdMetadata. A propriedade pode ser usada para ativar a pré-rolagem em um fluxo VoD. Se enableVodPreroll for NO, o PSDK não reproduzirá pre-roll. Isso, no entanto, não tem impacto sobre os cilindros médios. O valor padrão de enableVodPreroll é YES.
* closedCaptionDisplayEnabled API da interface PTMediaPlayer está marcada como obsoleta do iOS v1.4.43 em diante. Para determinar se as legendas ocultas estão disponíveis para um determinado PTMediaPlayerItem, examine a propriedade legendasOptions de PTMediaPlayerMediaItem.

**Versão 1.4.42**

Nenhum novo recurso é adicionado nesta versão. Para obter uma lista de problemas corrigidos, consulte Problemas resolvidos.

**Versão 1.4.41**

Alterações de API:

* **isSecure**: Uma nova API é introduzida para proteger o player de gravar e gerar um erro. O valor padrão é true.
* **allowExternalRecording**: Uma nova API é introduzida para permitir o espelhamento de airplay para um conteúdo seguro. O espelhamento Airplay é tratado como gravação, portanto, o valor allowExternalRecording deve ser definido como &#39;True&#39;, para permitir o espelhamento do airplay ou definido como &#39;False&#39; para interromper o espelhamento do airplay para conteúdo seguro. Por padrão, o valor é true.

**Versão 1.4.40**

Nenhum recurso novo.

**Versão 1.4.39**

* O iOS TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.
* O iOS TVSDK é atualizado para fazer solicitações de CRS do novo host Akamai `primetime-a.akamaihd.net`.
* A nova configuração de nome de host fornece delivery de ativo CRS por HTTP e HTTPS (SSL) em maior escala.

**Versão 1.4.36**

Integrar e certificar o VHL 2.0 no iOS TVSDK: Reduza a barreira na implementação da Biblioteca do VideoHeartbeats diminuindo a complexidade das APIs.

**Versão 1.4.34**

* Informações sobre anúncios de rede

   As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. A ID do anúncio, o sistema de anúncios e as extensões de anúncio VAST são fornecidos na `PTNetworkAdInfo` classe acessível por meio de uma `networkAdInfo` propriedade em um Ativo de anúncio. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como o **Moat Analytics**.

**Versão 1.4.31**

* **Métricas** de faturamento Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que o TVSDK gera um evento de start de fluxo, o start do player envia mensagens HTTP periodicamente para o sistema de faturamento do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

* **O suporte a vários CDN para** Ads CRStVSDK agora é compatível com vários CDN para anúncios CRS. Ao fornecer detalhes FTP para anúncios CRS, você pode especificar locais de CDN, diferentes do CDN padrão de propriedade do Adobe, como o Akamai.

**Versão 1.4.29**

Na classe PTSDKConfig, a API forceHTTPS foi adicionada.

A classe PTSDKConfig fornece métodos para aplicar o SSL em solicitações feitas aos servidores de decisão de anúncio da Adobe Primetime, DRM e Video Analytics. Para obter mais informações, consulte os métodos `forceHTTPS` e `isForcingHTTPS` nesta classe. Se um manifesto for carregado sobre HTTPS, o TVSDK preservará o uso de conteúdo de HTTPS e respeita esse uso ao carregar quaisquer URLs relativos desse manifesto.

**Observação**: As solicitações para domínios de terceiros, como pixels de rastreamento de anúncios, URLs de conteúdo e anúncios, e solicitações semelhantes não são modificadas, e é responsabilidade dos provedores de conteúdo e servidores de anúncios fornecer URLs compatíveis com HTTPS.

**Versão 1.4.18**

O Primetime iOS TVSDK agora é compatível com as criações do Javascript VPAID 2.0 para permitir uma experiência avançada de anúncios interativos em fluxo.

Para obter mais informações sobre o VPAID 2.0, consulte Suporte [a anúncios](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md)VPAID.

**Versão 1.4.17**

* tvOS

   O TVSDK suporta aplicativos nativos tvOS.
* Os seguintes tipos de conteúdo podem ser reproduzidos:

   * VOD
   * Live
   * AES-128
   * Áudio e legendas alternativas
   * FER

* Os seguintes tipos de anúncios podem ser exibidos:

   * Básico
   * VAST2
   * VAST3
   * VMA

* No momento, os seguintes recursos não são suportados:

   * Digital Rights Management (DRM)
   * Banners de anúncios
   * Linguagem de marcação de TV (TVML)

**Versão 1.4.13**

**Observação**: O módulo Nielsen foi removido da compilação TVSDK, o TVSDK será atualizado em breve com um novo módulo de integração Nielsen.

* **Anúncio de fallback, encadeamento de margarida na lógica de seleção de anúncios (Zendesk #3103)**

Para anúncios VAST (criativos) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Anúncio de fallback para anúncios](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md)VAST e VMAP.

**Versão 1.4.9**

* **Sinalização de Blecaute com Substituição de Conteúdo Alternativa**

Como parte da atualização 1.4 do TVSDK, agora também apoiamos a entrada e saída de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

**Versão 1.4.8**

* **Biblioteca do Video Heartbeats (VHL) atualizada para a versão 1.5**

   * Capacidade de enviar metadados com start de vídeo e/ou start de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - As pulsações são menores em média e menores em tamanho

**Versão 1.4.7**

* **Suporte para individualização no local**

Suporte para instalações no local do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para acessar um terminal diferente.

* **Proteção de saída baseada em resolução**

As Políticas de DRM agora podem especificar a resolução mais alta permitida, dependendo dos recursos de Proteção de saída do dispositivo. Por exemplo, &quot;Se o HDCP estiver disponível, permita que o conteúdo de resolução de até 1080p seja reproduzido e, se o HDCP não estiver disponível, permita que o conteúdo de resolução de até 480p seja reproduzido&quot;.

**Versão 1.4.4**

* **Atualização da Biblioteca do Video Heartbeats (VHL) para a versão 1.4.1.1**

   * Adicionada a capacidade de agrupar diferentes casos de uso de análises, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete. A quebra de anúncio é inferida das chamadas de método trackAdStart e trackAdComplete.
   * A propriedade playhead não é mais necessária ao rastrear anúncios.
   * Adicionado suporte para a ID do Visitante do Marketing Cloud.

* **Integração Nielsen SDK**

   * O TVSDK agora suporta o envio de beacons mTVR e MDPR ID3 para o SDK Nielsen sem qualquer integração personalizada. Para começar, baixe o SDK 3.1.2.19 do aplicativo Nielsen iOS.

**Versão 1.4.0**

* **Sinalização de Blecaute com Substituição de Conteúdo Alternativa**

   * Como parte da atualização 1.4 do TVSDK, o TVSDK também oferece suporte para entrar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remover/substituir anúncios C3**

   * Agora, nenhum trabalho de preparação adicional é necessário para inserir dinamicamente novos anúncios nos ativos VOD (Video-on-demand) que estão saindo da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova funcionalidade poderosa também é útil em casos em que o conteúdo ao vivo/linear é exibido durante a transmissão e é imediatamente suspenso para uso como conteúdo sob demanda sem tempo adequado para &quot;limpar&quot; o ativo.

## Certificação e suporte de dispositivos no 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Os seguintes recursos **não** são suportados no TVSDK:
>
>* Movimentação lenta, em qualquer plataforma ou versão.
>* Brincadeira ao vivo.


**Versão 1.4.43**

* O TVSDK 1.4.43 é certificado para iOS 11.

**Versão 1.4.29**

* O TVSDK 1.4.29 foi certificado para iOS 10.

**Versão 1.4.28**

* O TVSDK 1.4.28 foi certificado para iOS 10 Beta 7.
* Suporte a DRM para forçar HTTPS adicionando APIs forceHTTPS e isForcingHTTPS.
* As bibliotecas VHL foram atualizadas para 1.5.8, as bibliotecas Adobe Mobile para 4.8.4 e a biblioteca do utilitário logger para o público alvo de implantação versão 7.0.

**Versão 1.4.19**

Esta versão do TVSDK foi certificada com o Suporte FairPlay para iOS e tvOS.

**Versão 1.4.17**

* tvOS

   Esta versão do TVSDK inclui suporte para tvOS e foi certificada para fluxos HLS não criptografados.

   **Observação**: Lembre-se das seguintes diretrizes de compilação:

   * O suporte a tvOs TVSDK está limitado a fluxos criptografados não-Adobe DRM. Você deve remover a referência a drmNativeInterface.framework nas configurações de compilação tvOS. Ainda há suporte para fluxos criptografados AES.
   * A Apple exige que todos os aplicativos Apple TV tenham código de bits ativado, portanto, você deve ativar esse sinalizador nas configurações do projeto.

## Problemas resolvidos no 1.4 {#resolved-issues-in}

<!-- 

Comment Type: draft

<note type="note"> 
 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
</note>

 -->

<!-- 

Comment Type: draft

<note type="note"> 
 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
</note>

 -->

**Versão 1.4.45{#ios-tvsdk}**

* Ticket #36294 - TVSDK do iOS não funcional com o Xcode 10

   * Correção de problemas de compilação com o TVSDK no XCode 10. Devido aos requisitos do XCode 10, os aplicativos criados no TVSDK para iOS 1.4.45 e versões posteriores exigem um público alvo mínimo de implantação como iOS 7.0

* Ticket #36321 - Discrepância observada no intervalo pesquisável entre a instância PTMediaPlayer e AVPlayer no estado &quot;Reproduzindo&quot;.
* Ticket #36493 - suporte ao iOS 12 `libstdc++`

   * Correção de problemas de compilação com o TVSDK no iOS 12. Os aplicativos criados no TVSDK para iOS 1.4.45 e versões posteriores exigem um público alvo mínimo de implantação como iOS 7.0

**Versão 1.4.44**

* Ticket #34683 - O Tempo De Andamento Da Reprodução Do Anúncio Está Indo Negativo

   * Verificações adicionais feitas para lidar com o caso quando há uma incompatibilidade entre a duração reportada pelo servidor de anúncios e o conteúdo real do anúncio.

* Ticket #34801 - currentTime e localTime não estavam sendo atualizados ao buscar uma nova posição durante o status pausado

   * A hora atual do player pode ser definida como zero, caso o player esteja em estado de pausa; anteriormente, o tempo atual era definido como zero somente no estado de reprodução.

* Ticket #35037 - Reprodução parada com URL inválido ao retornar da inserção de anúncios com base em sinal.

   * Correção aprimorada fornecida para o problema fechado nº 34385 na versão 1.4.42. Adicionado isCancelado o código de controle de verificação e exceção para tornar a fila de operações mais robusta.

**Versão 1.4.43**

* (ZD#32990) - iOS: Reprodução de conteúdo em vez de publicidades em alguns pontos de sinalização. A API &#39;seletedMediaOptionInMediaSelectionGroup&#39; que fazia parte da interface AVPlayerItem foi movida agora sob AVMediaSelection no iOS 11. O problema foi resolvido usando essa nova API.
* (ZD#33683) TVSDK removido == sufixo das strings de metadados. O problema é corrigido na lógica de análise.
* (ZD#33905) - TVSDK do iOS fazendo chamadas para os arquivos manifest com dois agentes do usuário. O problema do agente do usuário foi corrigido na primeira chamada m3u8 (caso de instalação de limpeza). M3u8 tem os mesmos agentes de usuário para todas as chamadas agora.
* (ZD#34293) - Os pré-rolls inseridos em fluxos LINEAR não são reproduzidos corretamente no iOS11. O problema foi corrigido para anúncios de pré-rolagem.
* (ZD#34684) - Quando a política de ignorado do anúncio é aplicada, os quadros do anúncio precedente são exibidos por alguns segundos. Uma nova API, enableVodPreroll foi introduzida para desativar a reprodução de pré-rolagem na reprodução do vod. O valor padrão para esta API é &#39;Yes&#39;. A API garante a omissão da identificação do conteúdo do anúncio no conteúdo principal.
* (ZD#34765) - Após chamar stop(), poucos segmentos de Transmissão ainda são baixados. Aprimoramento da API Stop() para evitar o download dos segmentos extras.
* (ZD#34865) - Os anúncios anteriores ao livestream são truncados no iOS. Relacionado ao iOS11 e adicionar uma verificação adicional para confirmar se o fluxo é pré-roll ou conteúdo principal, trata desse problema.
* (ZD#35093) - Corrigido um cenário de failover em que, se a variante primária do fluxo falhar na inicialização (retorna 404), a reprodução não alterava para o fluxo de backup.

**Versão 1.4.42 (1.4.42.118)**

* (ZD#34385) - A reprodução é parada com um URL inválido ao retornar da inserção de anúncios com base em sinal.

   Aumente as contagens simultâneas máximas para CustomAVAssetLoaderOperations, para que as leituras do manifesto possam continuar a ser executadas.
* (ZD#34373) - Os usuários finais não podem transmitir fluxo para dispositivos conectados por HDMI, quando a gravação de fluxo é proibida.
* (ZD#32678) - O TVSDK não coleta as IDs de anúncio corretas no iOS.

   A ID do anúncio final do anúncio final agora é coletada em pings VHL no caso de redirecionamentos VAST/VMAP.
* (ZD#33904) - O TVSDK não está registrado para notificações AVFFoundation AVAudioSessionMediaServicesDidLostNotification e AVAudioSessionMediaServicesDidResetNotification.

   PTMediaServicesDidLostNotification e PTMediaServicesDidResetNotification agora podem ser registrados no aplicativo do player para obter as notificações quando os serviços de mídia são redefinidos ou perdidos.

* (ZD#33815) - Os clientes não podem atualizar suas regras de priorização e normalização do CRS sem exigir uma atualização do aplicativo.

   Adicionadas as APIs getCRSRulesJsonURL e setCRSRulesJsonURL ao iOS TVSDK.

**Versão 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemas ao criar o aplicativo de referência com o TVSDK versão 1.4.41

   A partir desta versão, o Xcode 9 é necessário para compilar o TVSDK para iOS.
* (ZD #29456) - Start de Airplay em estado de pausa

   Corrigido o problema de pausa que ocorria quando o vídeo pausava ao entrar na reprodução.
* (ZD #30371) - A hora do start AdBreak muda quando inserimos mais de 2 anúncios em fluxo linear

   Corrigido o erro ao tentar reproduzir conteúdo na Apple TV, que impede a reprodução completamente
* (ZD #32146)- Nenhum PTMediaPlayerStatusError é recebido para conteúdo do HLS Live ao bloquear o iOS 11 dev beta

   Nenhum PTMediaPlayerStatusError foi recebido para conteúdo HLS Live e VOD no bloqueio usando Charles (conexão Drop e 403)
* (ZD #29242) - Falha na reprodução de vídeo do Airplay com anúncios ativados

   Quando os anúncios são ativados e o AirPlay é ativado, iniciando a reprodução de um vídeo, a reprodução de vídeo nunca ocorre em start e nenhum erro é exibido
* (ZD#33341) - Os acionadores DRMInterface.h criam avisos no Xcode 9

   Correção de dois protótipos de bloco em DRMInterface.h que não tinham a palavra &quot;void&quot; em suas listas de parâmetro
* (ZD#31979) - Não compila/executa quando for iOS 10 ou posterior para iPhone 7/iPhone7+

   Correção: a compilação de documentos IB para anteriores ao iOS 7 não é mais suportada
* (ZD#32920) - Tela em branco em uma pausa de anúncio e sem conclusão de pausa de anúncio

   Quando uma pausa de anúncio apresenta instâncias de anúncio e uma instância de anúncio é concluída, uma tela em branco é exibida
* (ZD#32509) - Desativar gravação de tela do iOS 11 Desativar gravação de tela no iOS 11

* (ZD#33179) - Falha intermitente do evento no iOS11

   Corrigida a falha do evento no iOS 11

**Versão 1.4.40** (1.4.40.72)

* (ZD #32465) - O player não pode manipular listas de reprodução mescladas.

   Chamar completeLoadingWithError(com: Erro) para a fundação AV tentar o failover alternativo de streams/acionadores.

* (ZD #31951) - Erro de TVSDK durante Rotação de licença.

   Correção do problema de rotação de licença.
* (ZD #31951) - Tela em branco em uma pausa de anúncio e sem a conclusão da pausa de anúncio.

   Solucionado um problema em que os anúncios VPAID do Facebook costumavam retornar vários blocos CDATA em um único \&amp;lt;AdParameters\&amp;gt; nó VAST.
* (ZD #33336) - TVSDK do [iOS] - Os pods de anúncios não estão sendo preenchidos, apesar de o número de anúncios ser retornado pelo FreeWheel.

   Foi criada uma relação pai-filho entre o anúncio de sequência e o anúncio de fallback e a classificação com base na sequência principal e no índice.

**Versão 1.4.39** (1.4.39.43)

* (ZD #32178) - A versão TVSDK do iOS está incorreta.

   A saída da versão TVSDK nos arquivos de registro era 1.0.211. Foi corrigido para produzir a versão correta.

* (ZD #32199) - Carregamento lento do anúncio - O vídeo não é exibido para o conteúdo.

   A linha do tempo do Adbreak local que não estava sendo inicializado anteriormente é agora atualizada antes do uso.

* (ZD #27528) - Vídeo, áudio ou ambos congelam de 1 a 45 segundos após a reprodução de um ativo, se o áudio secundário estiver definido como não padrão no iOS 1.2.

   Prepare e informe as faixas de áudio no estado Pronto.

* (ZD #30411) - Você pode obter resultados inesperados, como sem áudio ou áudio incorreto, se escolher um idioma secundário do Sap.

   Prepare e informe as faixas de áudio no estado Pronto.

* (ZD #32199) - Carregamento lento do anúncio - O vídeo não é exibido para o conteúdo.

   A linha do tempo do Adbreak local que não estava sendo inicializado anteriormente é agora atualizada antes do uso.

* (ZD #27528) - Vídeo, áudio ou ambos congelam de 1 a 45 segundos após a reprodução de um ativo, se o áudio secundário estiver definido como não padrão no iOS 1.2.

   Prepare e informe as faixas de áudio no estado Pronto.

* (ZD #30411) - Você pode obter resultados inesperados, como sem áudio ou áudio incorreto, se escolher um idioma secundário do Sap.

   Prepare e informe as faixas de áudio no estado Pronto.

**Versão 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Adicionar AdSystem e Creative Id a solicitações CRS

Utilização de ID criativo e AdSystem na solicitação de CRS com base nas regras de normalização de CRS

* (ZD #29176) - Falha no PTAdPolicyIdentiate satAdBreakAsWatched:position

Falha devido a AdBreak vazio é tratada agora.

* (ZD #30125) - Anúncios programáticos não estão funcionando na plataforma iOS

Adição de suporte a anúncios programáticos no iOS.

* (ZD #30782) - #EXT-X-PROGRAMA-DATE-TIME Notification

O evento de metadados cronometrados não é disparado para a tag # EXT-X-PROGRAMA-DATE-TIME com fluxos DRM ao vivo.

**Versão 1.4.37 (1.4.37.842)**

* (ZD #28950 ) - Problema de reprodução VOD

Problema de reprodução quando a tag # EXT-X-PLAYLIST-TYPE no fluxo é definida como Evento em vez de VOD

* (ZD #29281) - iOS: Adicionar AdSystem e Creative Id a solicitações CRS

Uso da ID criativa e AdSystem na solicitação de CRS com base nas regras de normalização do CRS.

* (ZD #29462) - Anúncio do TremorHub no VOD A&amp;E que causa uma falha nos aplicativos iOS

**Versão 1.4.36 (1.4.36.835)**

* (ZD #29418) - Os casos com duração 0 (#EXT-X-CUE-OUT:0.000) estão fazendo com que o iOS TVSDK pare ou trave a reprodução.

O problema foi corrigido e os start de reprodução foram executados corretamente.

* (ZD #29462) - Anúncio no VOD que causa uma falha no iOS TVSDK.

O problema foi corrigido. O TVSDK do iOS está gerando uma exceção (AUDNetworkAdInfo::initWithAdId) e não manipulando-a. A exceção se deve a uma ID de anúncio vazia.

* (ZD #29281) - Adicionar AdSystem e ID criativa a solicitações CRS.

Inclua AdSystem e CreativeId como novos parâmetros nas solicitações 1401 e 1403 (todos os outros parâmetros permanecem os mesmos).

**Versão 1.4.35** (1.4.35.830)

* (ZD #27830) - Precisa determinar programaticamente a diferença entre legendas e legendas no iOS.

O TVSDK agora expõe os dois tipos que podem ser usados para filtrar o tipo de legenda necessário.

* (ZD #29160) - As dicas de anúncio EXT-X-CUE-OUT não são sincronizadas corretamente no TVSDK iOS.

Com EXT-X-CUE-OUT, o anúncio do midroll está sendo reproduzido agora.

* (ZD #29100) - O aplicativo falha quando o usuário navega até o final de um filme.

Corrigidas várias falhas relacionadas à sincronização.

* (ZD #28785), (ZD #27712) e (ZD #25076) - o aplicativo iOS está travando durante os grandes eventos ao vivo.

Corrigidas várias falhas relacionadas à sincronização.

**Versão 1.4.34** (1.4.34.815 para iOS 6.0+)

* (ZD# 28481) - Fim da FER devido à chave incorreta ser anexada no final de uma pausa de anúncio para esses fluxos FER

Para um fluxo FER, a tecla antes do intervalo do anúncio é inserida após o fim do intervalo do anúncio. Esse problema foi resolvido ao anexar a *última chave* vista no final do intervalo do anúncio.

**Versão 1.4.33** (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Ativar CRS para subcontas

Habilitado enviando o URL criativo original para a solicitação CRS 1401 em vez do URL normalizado, de acordo com o requisito de back-end CRS.

* (ZD# 26218) - Problema de carregamento PSDKResources.bundle

Esse problema foi resolvido atualizando o carregamento de recursos para procurar de todos os pacotes disponíveis.

* (ZD# 27460) Primeira chamada de anúncio do Midroll - POST para cdn.auditude<span></span>.com retornando 403.

A nova conta CDN não consegue processar uma solicitação de CDN POST. Esse problema foi resolvido com a atualização do código para fazer com que a solicitação de `cdn.auditude.com` anúncio fosse GET em vez de POST.

**Versão 1.4.32** (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Suporte para valores decimais para quebras de anúncio VMAP.

Quando o conteúdo não era segmentado ao longo das quebras de anúncio definidas, os números inteiros causavam posicionamentos de anúncio inesperados. O problema foi resolvido ao não converter os valores decimais em números inteiros.

* (ZD# 27189) O conteúdo AES com a tag EXT-X-DISCONTINUITY-SEQUENCE não está sendo reproduzido corretamente.

O problema foi resolvido colocando a tag no início da lista de reprodução.

**Versão 1.4.31** (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar métricas de uso do TVSDK para faturamento

Para obter mais informações, consulte Métricas [de](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md)faturamento.

* (ZD# 24642) Suporte Picture-in-Picture para TVSDK

O recurso picture-in-picture, que não estava funcionando corretamente em alguns casos, foi corrigido.

* (ZD# 25246) Sinais Incorretos De Quebra De Anúncio

Esse problema foi solucionado ao alinhar tags de descontinuidade em manifestos de variantes.

* (ZD# 26218) O processo de compilação do aplicativo fica complicado ao tentar incluir PSDKLibrary.framework na estrutura do aplicativo do cliente

Esse problema foi resolvido com o empacotamento do PSDKLibrary.framework, conforme solicitado.

* (ZD# 26364) Suporte a vários CDN para anúncios de CRS

<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Atraso na reprodução de alguns fluxos no iOS 10.

Esse problema foi resolvido fornecendo uma solução alternativa para fluxos que não têm uma extensão M3U8.

**Versão 1.4.30** (1.4.30.754 para iOS 6.0+)

Os seguintes problemas foram resolvidos para o TVSDK nesta versão:

* (ZD# 24180) Adicionar um cabeçalho personalizado à lista de permissões

Um novo cabeçalho personalizado foi adicionado à lista de permissões TVSDK.

* (ZD# 25016) O fluxo de failover é selecionado aleatoriamente quando os parâmetros de controle ABR são definidos

Esse problema foi resolvido com a manutenção dos fluxos ABR em ordem quando as configurações ABR são fornecidas com a configuração inicialBitrate em um fluxo que inclui URLs de failover. Isso evitará reproduzir os fluxos de failover em vez do primário.

* (ZD# 25076) Falha em PTAuditudeAdResolver loadComplete

Foi corrigido o problema em que uma falha ocorria durante um start/parada rápido de várias instâncias de PTMediaPlayer com anúncios.

* (ZD# 25960) Nenhuma tara adicional subscrita acionando transmissões de notificação de alteração de metadados

O problema no qual uma tag assinada não é notificada quando aparece antes do primeiro segmento no manifesto foi corrigido.

* (ZD# 26084) PSDK lançando um 106000.101000.O decodificador -11833 não encontrou erro ao migrar do último anúncio para o conteúdo de entretenimento

Quando o último start de intervalo de anúncio do VMAP cair antes da duração total ser concluída, em determinadas condições, a tecla não será inserida até o final do último intervalo de anúncios. Esse problema foi corrigido.

* A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

   * (ZD #22351) VHL - Analytics: Duração de ativos de vídeo ao vivo

Esse problema foi resolvido adicionando a API assetDuration para `PTVideoAnalyticsTrackingMetadata` atualizar a duração do ativo para fluxos ao vivo/linear e fornecer uma lógica para a verificação do fluxo ao vivo.

* (ZD# 22675) VHL - Analytics: Atualização da duração de ativos de vídeo ao vivo

Esse problema é igual ao ZD #22351.

* (ZD #25908) VHL - Analytics: Falha no Evento do Adobe Heartbeat

Esse problema foi resolvido com a atualização da implementação para usar a versão mais recente do VHL para iOS versão 1.5.9 para melhorar a estabilidade e o desempenho.

* (ZD #25956) VHL - Analytics: Falha ao reproduzir vídeos repetidamente

Esse problema é o mesmo que ZD #25908.

**Versão 1.4.29** (1.4.29.743)

* (ZD# 23901) Anúncios de terceiros não estão sendo reproduzidos

Esse problema foi resolvido ao mover-se para a estrutura de URL CRS v3 para incluir a ID da zona no URL reempacotado.

* (ZD #25183) Problemas com a reprodução de DRM no tvOS e iOS

Esse problema foi solucionado fornecendo suporte para várias tags-chave que são necessárias para o suporte a vários DRM.

* (ZD# 25334) O TVSDK falha ao reproduzir um conteúdo compartilhado cDVR

Esse problema foi resolvido impedindo o TVSDK de converter sequências vazias em URLs absolutos.

* (ZD# 25347) Definir cabeçalho HTTP personalizado em AVURLAsset

Foi adicionado suporte para cabeçalhos personalizados em suas solicitações de segmento por meio da classe PTNetworkConfiguration.

**Versão 1.4.28** (1.4.28.722)

* (ZD #24549) Várias chamadas de rastreamento de anúncio

Esse problema foi solucionado atualizando o gerenciador de linha do tempo para ouvir notificações em um objeto específico quando vários players são criados.

* (ZD #24758) PTManifestLogger não suporta iOS 8

Esse problema foi resolvido com a atualização da biblioteca do utilitário logger para o público alvo de implantação da versão 7.0.

* (ZD #24775) Fluxo atrasado devido a anúncios

Esse problema foi resolvido calculando corretamente o desvio de duração nas listas de reprodução do evento.

* (ZD #24799) Alguns dos episódios não estão sendo reproduzidos no iOS APP

Esse problema foi resolvido usando o servidor Web local para legendas quando os arquivos WebVTT eram restritos geograficamente.

**Versão 1.4.27** (1.4.27.711) para iOS 6.0+

* (ZD #24089) - Otimizações para a resolução de anúncios em fluxos de DVR longos

Esse problema foi resolvido com a adição de várias otimizações para reduzir o tempo necessário para processar a janela do DVR em fluxos ao vivo/lineares.

* (ZD #21554) - Beacons de erro TVSDK não acionados para o tipo de aplicativo = video/mp4

Esse problema foi resolvido permitindo que o player execute ping nos URLs de rastreamento de erros corretos em formatos de ativos inválidos.

* (ZD #24424) - Falha do tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS tem origem em PSDKLib para iOS em dispositivos de hardware mais recentes.

A falha que ocorria devido a uma instância de media player desalocada, quando a reprodução é alternada rapidamente entre diferentes fluxos, foi corrigida.

* (ZD #24575) - Falha no TVSDK em dispositivos de 32 bits quando enableDebugLog=true

O problema no formato de log que causou a falha em dispositivos de 32 bits quando o registro está ativado foi corrigido.

**Versão 1.4.26** (1.4.26.702) para iOS 6.0+

* (ZD# 20213) - O FW TVSDK precisa ser dinâmico/modularizado para XCode7

   * Corrigido ao atualizar as bibliotecas com suporte a módulo

**Versão 1.4.25** (1.4.25.684) para iOS 6.0+

* (ZD #19629) - Vídeo ao vivo pausa ao entrar no Airplay para ATV 4

Esse problema foi resolvido adicionando um período de espera após a remoção de itens antigos, mas antes de adicionar novos itens ao AVQueuePlayer. Sem o período de espera, as notificações são enviadas para o item incorreto.

* (ZD #19856) - Nenhuma legenda é exibida quando ativada por padrão

Os problemas na lista de reprodução de webvtt, que fazia com que as legendas não fossem exibidas corretamente, foram corrigidos.

* (ZD #21590) - Desempenho e rastreamento de vídeo nas mais recentes compilações de Origem

O problema sobre a duração do vídeo ausente no VideoAnalytics foi corrigido.

* (ZD #20202) - A definição de legendas personalizadas como estilo trava o aplicativo iOS

Esse problema foi resolvido adicionando verificações de objeto nulo adicionais ao configurar estilos de legenda.

* (ZD #20709) - duração do vídeo reportada como 0 no rastreamento de start de vídeo

Esse problema é o mesmo que (ZD #21590).

* (ZD #22280) - Duração do vídeo do Analytics definida como 0

Esse problema é o mesmo que (ZD #21590).

* (ZD #22592) - Problemas com o Airplay no Primetime

Esse problema é o mesmo que (ZD #19629).

* (ZD#22922) - Alternância manual da taxa de bits para iOS

Esse problema foi resolvido fornecendo uma opção para especificar a taxa de bits máxima.

* (ZD #23084) - Conformidade da Apple para redes somente IPv6

Os símbolos que não foram recomendados pela Apple para compatibilidade IPv6 foram removidos.

**Versão 1.4.24** (1.4.24.661) para iOS 6.0+

* ZD #2548) - Suporte Primetime para publicidade interativa em dispositivos móveis - VPAID 2.0

Esse problema foi resolvido atualizando a lógica para mostrar a visualização do player se um anúncio VPAID não for reproduzido.

* (ZD #20101) - A implementação do Capítulo personalizado aciona o evento do capítulo do start durante a reprodução do anúncio

Esse problema foi solucionado ao atualizar o VideoAnalyticsTracker para detectar corretamente o start/conclusão do capítulo ao fazer a transição entre os limites do capítulo e não capítulos.

* (ZD #20784) - Analytics: Acionar conclusões de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido com a adição de uma lógica para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo.

As seguintes bibliotecas foram atualizadas:

* Biblioteca do AdobeMobile para 4.10.0
* Biblioteca VHL para 1.5.6
* Biblioteca VHL-Nielsen para 1.6.7
* (ZD #21855) - As legendas não são reproduzidas após o mid-roll

Nesse problema, as tags de descontinuidade de duplicado faziam com que as legendas não aparecessem depois da rolagem média. Esse problema foi resolvido com a remoção das tags de descontinuidade próximas.

* (ZD #21994) - String fora dos limites em PTHLSUtils

A causa mais provável da falha é quando uma EXT-X-KEY tem um URL entre aspas.

* ZD #22074) - Falha AUDVAST ocorrendo uma vez por minuto no iOS

Na versão 1.4.23, a falha causada pela presença de caracteres não seguros em um URL de redirecionamento VAST foi corrigida. No entanto, o TVSDK continuava ignorando esses anúncios.

Esse problema foi resolvido com o manuseio de caracteres não seguros e permitindo que os anúncios sejam reproduzidos.

* (ZD #22694) - PTMediaPlayer.  Visualização oculta pelo player

Esse problema foi resolvido atualizando a lógica para mostrar a visualização do player se um anúncio VPAID não for reproduzido.

**Versão 1.4.23** (1.4.23.641) para iOS 6.0+

* (ZD #18016) - Nenhuma resposta do Primetime SDK com uma condição de rede incorreta

Esse problema foi resolvido melhorando a notificação de erro quando ocorre um erro fatal do AVFFoundation e permitindo que o aplicativo gerencie a reinicialização após o erro.

* (ZD #20580) - Falha no PTSplicerManager

Esse problema foi resolvido fornecendo proteção adicional contra problemas de simultaneidade que causam o travamento.

* (ZD #21782) - Código de erro 10100 do iOS

Foi corrigido o problema em que o TVSDK retornava um erro 101000 ao iniciar a reprodução em fluxos de DRM de acesso ao Adobe.

* (ZD #21889) - Falha na reprodução de anúncios online e conteúdo offline

O problema no qual a reprodução falhava após um anúncio de conteúdo offline criptografado por AES ter sido corrigido.

* (ZD #22074) - Falha do AUDVAST ocorrendo uma vez por minuto no iOS

Esse problema foi resolvido melhorando o tratamento de tags de anúncios VAST de terceiros que têm caracteres inválidos no URL.

* (ZD #22257) - O TVSDK falha ao reproduzir o fluxo DRM

O problema no qual o TVSDK que retornava um erro 101000 ao iniciar a reprodução em fluxos de DRM de acesso ao Adobe foi corrigido.

**Versão 1.4.22** (1.4.22.627) para iOS 6.0+

* (ZD #18709) - Falha no TVSDK para iOS

O problema de travamento que ocorre em alguns fluxos protegidos por DRM de acesso a Adobe foi corrigido.

* (ZD #18850) - Atualizar lógica de seleção criativa com base nas regras do CRS

Esse problema foi resolvido com a adição de um arquivo de configuração .json para especificar a prioridade de seleção criativa.

* (ZD #19770) - Feed de vídeo AES protegido que não está mais sendo reproduzido

Foi corrigido o problema em que certos streams redirecionados 302 estavam falhando em ser reproduzidos.

* (ZD #19629) - Vídeo ao vivo pausa ao entrar no Airplay para ATV 4

Esse problema foi resolvido com a adição de uma solução alternativa para pausa de vídeo ao vivo quando a reprodução do ar está ativada para dispositivos Apple TV 4. O problema parece ser um problema da AppleTV 4.

* (ZD #21119) - O TVSDK é parado após a reprodução do anúncio

O suporte foi adicionado para fluxos criptografados por AES com uma sequência IV ao usar a inserção do anúncio.

* (ZD #21125) - Retorno de uma pausa de anúncio ao vivo/linear antecipada

O suporte foi adicionado para retornar de uma pausa de anúncio cedo antes de a pausa de anúncio ser reproduzida até a conclusão. O retorno antecipado é indicado por meio de uma tag manifest personalizada.

* (ZD #21224) - Suporte a Airplay para fluxos canalizados do Akamai

As APIs foram adicionadas à classe PTNetworkConfiguration para anexar cookies como parâmetros de URL em segmentos para determinados fluxos de tokens do Akamai.

* (ZD #21287) - Registro de erros

Foi corrigido um problema com algumas declarações de log exibidas por padrão no console do xcode mesmo quando o registro está desativado.

* (ZD #21446) - eventos de quebra de anúncio às vezes não acionados pelo TVSDK

Em fluxos de EVENTO, as quebras de anúncio não são acionadas corretamente na versão anterior. Essa compilação aborda esse problema.

**1.4.21** (1.4.21.605) para iOS 6.0+

* (ZD #20749) - O fallback ignora respostas VAST não vazias; URLs de rastreamento de anúncio extras são acionados

Um problema com duplicados nos anúncios de fallback foi resolvido.

**1.4.20** (1.4.20.590) para iOS 6.0+

* (ZD #18639) - O TVSDK está usando CPU/recursos excessivos em um ativo de gravação automática demorado

A utilização excessiva de CPU/recursos foi corrigida nos dois níveis. Primeiro, permitindo que a função de atualização de tempo seja executada em uma fila global, em vez do thread principal, e otimizando o uso da CPU para analisar o manifesto com o m3u8 processado e armazenado em cache anteriormente.

* (ZD #19349) - Os anúncios anteriores ao roll estão sendo ignorados ao restringir a conexão de rede.

Esse problema foi resolvido fornecendo um evento de tempo limite (requestTimeout) ao aplicativo e ao adMetadata.  adRequestTimeout API para substituir o tempo limite padrão de 10 segundos.

* (ZD #19446) - Notificação ausente em fluxos ao vivo

Esse problema foi resolvido ao permitir que o aplicativo assinasse o EXT-X-PROGRAMA-DATE-TIME em fluxos ao vivo.

* (ZD #19459) - Falha ao preparar áudio alternativo com PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Travamento - [PTMediaPlayerItem prepareLegendasOpçõesComAVMediaSelectionOptions:nonForcedOptions:]

Este problema é o mesmo que Zendesk #19459.

* (ZD #19574) - O TVSDK não está retornando dados de resposta M3U8 para conteúdo DRM ou não-DRM

No carregamento inicial do arquivo manifest em PTMediaPlayerItem.prepareToPlay, se o carregamento do manifesto falhar, o TVSDK não informa o corpo da resposta de falha ao aplicativo.

Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro para o aplicativo.

* (ZD #19615) - A lógica de fallback não está funcionando

Na implementação atual, os anúncios de fallback foram ignorados e não foram reempacotados, a menos que esses anúncios estejam no formato m3u8. Esse problema foi resolvido com a adição do suporte para reempacotamento de anúncios de fallback.

* (ZD #19770) - O TVSDK falha ao reproduzir qualquer conteúdo protegido do AES com o redirecionamento 302

O problema de redirecionamento foi corrigido, pois o URL de redirecionamento estava sendo eliminado por cleanConnectionData antes de poder ser usado para analisar o manifesto.

* (ZD #19856) - As legendas não são exibidas para algumas taxas de bits quando ativadas por padrão

Esse problema foi resolvido com a manipulação do erro do iOS para os segmentos dos fluxos nos quais as legendas não são exibidas.

* (ZD #19868) - O TVSDK falha quando um anúncio inválido é acessado por tráfego

A falha no TVSDK que estava desalocando incorretamente uma instância do analisador vasto foi corrigida.

* (ZD #20180) - Anúncios VPAID são ignorados ocasionalmente

O tipo mime JavaScript nem sempre estava sendo incluído ou considerado como um tipo mime válido. Esse problema foi resolvido com a inclusão do JavaScript como um tipo mime válido.

* (ZD #20749) - O fallback ignora respostas VAST não vazias; URLs de rastreamento de anúncio extras são acionados

O problema em que alguns dos criativos não estão sendo reembalados foi resolvido.

**Versão 1.4.19** (1.4.19.563) para iOS 6.0+

* ZD #18639) - O TVSDK usa CPU/recursos excessivos em um ativo de gravação automática demorado

Esse problema foi resolvido com a otimização da regravação da lista de reprodução do DRM m3u8 em bits de cache da lista de reprodução que foram previamente reescritos. Isso é mais relevante quando você reproduz fluxos em tempo real m3u8 para os quais o m3u8 é baixado após cada download de segmento.

* (ZD#18956) - player.drmManager é nulo quando o ponto de interrupção é definido no iOS Demo Player

Esse problema foi resolvido com a atualização da implementação da API PTMediaPlayer.drmManager para coletar o DRMManager da estrutura DRM.

**Versão 1.4.18** (1.4.18.557) para iOS 6.0+

* (ZD #18844) Rastreamento do indicador de reprodução para conteúdo ao vivo no iOS player.

Esse problema foi resolvido permitindo que os aplicativos definissem seu próprio valor de indicador de reprodução.

* Zendesk #18518 - Se o nome do vídeo não for especificado, o nome do TVSDK assumirá como padrão o player baseado em *PSDK.*

Esse problema foi resolvido com a remoção do valor padrão do nome do player.

**Versão 1.4.17** (1.4.17.545) para iOS 6.0+

* Zendesk #2228 - Aprimorar o TVSDK para retornar a resposta JSON da busca de um manifesto

Em vez de enviar um erro quando o conteúdo não é M3U8, a Estrutura DRM retorna um DRMMetadata nulo. O problema foi resolvido com a adição de metadados para expor o conteúdo quando ocorre a notificação M3U8_PARSER_ERROR.

* Zendesk #2231 - Erro retornado ao buscar o manifesto indisponível no MediaPlayerNotification

Mesma resolução do Zendesk nº 2228

* Zendesk #3304 - macro VAST 3.0 `[ERRORCODE]` não sendo preenchida

O problema no qual o SDK do Auditude não envia um ping quando o URL de rastreamento tem espaços no início foi resolvido.

* Zendesk #17294 - Falha no SecKeyRawSign

Uma possível falha quando o código do cliente usa a cadeia-chave foi resolvida.

* Zendesk #18008 - Cookies de suporte para iOS8+ para dar suporte a fluxos tokenizados

O Akamai tokenized streams requer que os cookies sejam enviados em solicitações de segmento, o que não foi possível no iOS 7 e anterior. A partir do iOS 8, a Apple adicionou uma API que permite que os cookies sejam enviados para solicitações de segmento. Esse suporte agora está disponível no TVSDK. O suporte também foi adicionado para enviar um agente-usuário, se disponível.

* Zendesk #18166 - TVSDK 1.4.15 fornece centenas de avisos ao compilar com o DWARF com opções de arquivo dSYM

Todos os avisos foram resolvidos.

**Observação**: bibliotecas compatíveis com tvOS foram adicionadas para TVSDK.

**Versão 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S Crash durante a reprodução

Reverter a dependência de OKHTTP na auditude para CRS porque o TVSDK agora está usando diretamente a httpurlconnection em vez de curl. O problema foi resolvido com a compensação de exceções antes de fazer outra chamada JNI.

* Zendesk #4487 - Rastreamento do Canal linear do conteúdo

O problema foi resolvido reinicializando o rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17919 - Android - busca de conteúdo causa erro de pulsação

O problema era resolver a pulsação em um estado de erro quando há uma busca em um capítulo

* Zendesk #18053 - O aplicativo que usa o TVSDK trava no Marshmallow

O TVSDK falhava no Android M OS quando a biblioteca do TVSDK usa um código neon que faz a conversão de cores YUV -> RGB. Esse problema foi resolvido com a atualização das funções que estão causando esse problema usando uma versão não neon do código.

* Zendesk #18072 - Android M - Travamento do aplicativo

Essa falha ocorre ao chamar as APIs MediaCodecList e MediaCodecInfo ao verificar se o perfil e o nível são suportados. A Adobe está buscando o suporte do Google para obter informações adicionais. Esse problema foi resolvido fornecendo uma solução temporária carregando todas as informações do codec antecipadamente para evitar chamar essas APIs somente quando as informações do codec forem necessárias.

* Zendesk #18074 - Legendas árabes que não funcionam no Nexus com Android 6.0

Esse problema foi resolvido fornecendo suporte para o mapa de fontes CTS do Android.

**Versão 1.4.15** (1.4.15.512) para iOS 6.0+

**Observação**: O módulo Nielsen foi removido da compilação TVSDK, mas o TVSDK será atualizado em breve com um novo módulo de integração Nielsen.

* (ZD #2228) - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification

Metadados adicionados para expor conteúdo quando ocorre a notificação M3U8_PARSER_ERROR.

* (ZD #4437) - Falhas no Adobe Primetime SDK

Corrigida uma falha relatada ao preparar legendas/áudio alternativo.

* (ZD #4487) - Rastreamento do Canal linear do conteúdo

A reinicialização do rastreador de pulsação de vídeo foi permitida durante uma sessão de reprodução de fluxo linear.

**Versão 1.4.14** (1.4.14.498) para iOS 6.0+

* (ZD #17260) - Travamento na playlistManagerForURL

Corrigida uma falha intermitente devido a problemas de simultaneidade.

**Versão 1.4.13** (iOS 6.0+)

* (ZD #3304) - `[ERRORCODE]` macro VAST 3.0 que não está sendo preenchida

   * O código de erro 400 será exposto se o anúncio em linha apresentar anúncios mal criados.
   * `[ERRORCODE]` a macro será codificada no URL.

* (ZD #3865) Integração do Heartbeat com anúncios IMA

Correção de um erro em que a duração do vídeo era relatada incorretamente.

* Reprodutor de demonstração TVSDK atualizado para suportar iOS 9

Para suportar adequadamente o iOS 9, é necessário configurar as exceções do Application Transportation Security. Para o objetivo da demonstração, o ATS é completamente desativado.

**Versão 1.4.12** (1.4.12.464) para iOS 6.0+

* (ZD #4521) CRS Testando o lado do cliente e o SSAI

Correção de MD5 reverso incorreto no URL 3P.

**Versão 1.4.12** (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI e CRS | Reforço: Tratar elementos dinâmicos em determinados URLs de arquivos de mídia.

Serviço de reempacotamento da Creative para lidar corretamente com anúncios com URLs criativos dinâmicos.

* (ZD #3654) Vazamento de memória na versão PSDK após 1.3.4.166

Foi corrigido um vazamento de memória no drmFramework com reprodução regular em dispositivos iOS 8.2

* (ZD #3988) A pré-rolagem é ignorada ao buscar novamente nele após a primeira reprodução

Correção de um erro para que as políticas de publicidade pudessem ser desativadas corretamente.

* (ZD #4017) Solicitação da API iOS para forçar a reprodução do anúncio em busca retroativa

Solução com correção para ZD #4279

* (ZD #4279) HLS TVSDK adição inserção -302 problema de redirecionamento no iOS e na área de trabalho

Corrigido o bug quando um ativo de anúncio estava usando um URL de redirecionamento relativo

**Versão 1.4.9** (1.4.9.427) para iOS 6.0+

* (ZD #3075) Problema de acessibilidade à Internet - iOS

Foi adicionada uma notificação para detectar quando a reprodução parou.

* (ZD #3193) Solicitação de uma API de alteração de Perfil no TVSDK

Atualização de PTPlaybackInformation para expor a taxa de bits indicada atualizada. Atualização da notificação BITRATE_CHANGE para que seja mais confiável e precisa para as taxas de bits M3U8 relatadas.

* (ZD #3324) Problema de relatórios de anúncios do Primetime quando não há mídia de anúncio no VMAP

Suporte para fazer ping de URLs de rastreamento de quebra de anúncio vazios, o TVSDK agora verificará o start de quebra de anúncio e concluirá os pings para quebras de anúncio vazias

**Versão 1.4.8** (1.4.8.402)

* (ZD #3158) O IOS 7 falha em reproduções de Evento completo

**Versão 1.4.7** (1.4.7.382)

* (ZD #2197) Rastrear erros de anúncio. A notificação adicionada para o ativo falhou ao carregar o manifesto.
* (ZD #2894) O Player faz 4 solicitações de manifesto de nível superior durante a reprodução.
* (ZD #2992) Durações e identificadores estranhos do Relatórios Auditude.

**Versão 1.4.6**(1.4.6.325)

* (ZD #2197) Rastrear erros de anúncio. Falha ao carregar a notificação do ativo adicionada para o manifesto

**Versão 1.4.5** (1.4.5.283)

* (ZD #2141) Implementação do Analytics para o aplicativo TreeHouse, adicionou a biblioteca AdobeAnalyticsPlugin.a para criar o pacote.
* Atualização da biblioteca do Video Heartbeats para 1.4.1.2
* (PTPALY-4226) (relacionado ao ZD #2423) A execução da redefinição de DRM pode resultar na exclusão dos dados do Documento do aplicativo.

**Versão 1.4.4** (1.4.4.242)

* A Biblioteca do Video Heartbeats (VHL) é atualizada para 1.4.1.

* (ZD #2435) A documentação do SDK da TV sobre análises precisa de atualizações

**Versão 1.4.2** (1.4.2.2010: iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOpções retornando vazio
* (ZD #2109) O Primetime PSDK 1.4.1.125 não funciona com o Xcode 5.1.1
* (ZD #2137) Falha no PSDK no iOS quando os metadados do DRM não podem ser carregados

**Versão 1.4.1** (1.4.1.125)

* (ZD #1107) Símbolos de duplicado CocoaLumberjack
* (ZD #1644) Modificar o agente de usuário do iOS para segmentação e Relatórios
* (ZD #1850) Arquivos Cocoa Lumberjack incluídos no SDK do iOS
* (ZD#1908) Tags personalizadas são ignoradas pelo PSDK se houver mais de 1

**Versão 1.4.0** (1.4.0.32)

* Zendesk #1024 - Recurso para remover anúncio do fluxo via manifesto

## Problemas conhecidos no 1.4 {#known-issues-in}

* No iOS TVSDK, todos os anúncios são agrupados no manifesto do conteúdo. Os comportamentos de publicidade são implementados buscando com base na duração do conteúdo e dos segmentos de anúncios. Portanto, se a duração do segmento não for precisa, a busca pode nem sempre terminar no quadro exato do início ou do fim do intervalo do anúncio. Mesmo se as durações forem para o quadro, há uma tolerância que a própria plataforma impõe à busca e pode haver alguns quadros ou anúncios ou conteúdos exibidos. Essa é uma limitação da plataforma e a maneira como a inserção de anúncios funciona com TVSDK no iOS.
* A decisão de ignorar acontece no evento de busca neste caso. No entanto, como as durações do segmento de anúncio no manifesto não representam com precisão a duração real do anúncio, a busca não é precisa de quadros. Assim, você verá alguns quadros do anúncio quando as políticas de publicidade forem aplicadas.
* RECORDING_ERROR: Ocorreu um erro ao gravar a tela.
* Pode ser que o vídeo de rotação de licença não seja reproduzido no iOS 11 e será reproduzido corretamente no iOS 9.x e no iOS 10.x.
* No suporte a VPAID 2.0, se a reprodução estiver ativa no AirPlay, os anúncios VPAID serão ignorados.
* O drmNativeInterface.framework não é vinculado corretamente quando o público alvo mínimo está definido como iOS7 (ou posterior).\
   Solução: Especifique o `libstdc++6`.  biblioteca dylib, como se segue: Vá para Público alvo->Criar fases->Vincular binário com bibliotecas e adicione `libstdc++.6.dylib`.

* Anúncio pós-rolagem não é inserido para substituir a API.
* A busca por uma pausa de anúncio (sem sair dela) emite uma notificação de start de anúncio de duplicado e quebra de anúncio
* A definição de currentTimeUpdateInterval não tem nenhum efeito.\
   Observação: Em determinadas versões do iOS, o SO não carrega os recursos dentro do PSDKLibrary.framework automaticamente. É importante copiar manualmente o PSDKResources.bundle para os recursos de pacote do aplicativo: Vá para &quot;Criar fases&quot; e copie os recursos do pacote.
* Não é possível criar o aplicativo de referência usando o Xcode 8 ou versões anteriores. A partir do iOS TVSDK versão 1.4.41, use o Xcode 9 para compilar.

## Recursos úteis {#helpful-resources}

* Consulte a documentação completa da ajuda na página Aprendizagem e suporte [da](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.