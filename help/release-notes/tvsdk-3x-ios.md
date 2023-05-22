---
title: Notas de versão do TVSDK 3.13 para iOS
description: As Notas de versão do TVSDK 3.13 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK iOS 3.13.
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# Notas de versão do TVSDK 3.13 para iOS {#tvsdk-for-ios-release-notes}

As Notas de versão do TVSDK 3.12 para iOS descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK iOS 3.12.

## Requisitos de sistema e software {#system-software-requirements}

Antes de baixar o iOS 3.12, verifique se as versões de hardware, sistema operacional e aplicativo atendem aos seguintes requisitos:

Sistema operacional: iOS 8.0 ou posterior.

## iOS TVSDK 3.13

A versão apresenta suporte para anúncios DEMUXED &#39;HLS/CMAF&#39; (pré-rolagem, midroll e postroll) para fluxos LIVE, VOD e FER.

Para correções de problemas relatados pelos clientes, consulte [Problemas resolvidos](#resolved-issues). Para ver as limitações, consulte [problemas conhecidos e limitações](#known-issues-and-limitations).

### Novos recursos e correções nas versões anteriores {#whats-new-previous}

**iOS TVSDK 3.12**

Correção de um problema em que o stream ao vivo falha após 15 minutos de reprodução.

**iOS TVSDK 3.11**

Foram fornecidas correções para problemas de clientes em que `isFallbackOnInvalidCreativeEnabled` e método `customParams` causa falha do aplicativo.

**iOS TVSDK 3.10**

* Correção de um problema em que o reprodutor TVSDK não é acionado `PTMediaPlayerStatusError` notificação quando a rede não estiver disponível.

**iOS TVSDK 3.9**

* Correção de um problema em que as legendas em VTT não eram reproduzidas, causando o congelamento do aplicativo.

* O iOS TVSDK 3.9 incluiu o certificado de transporte de individualização atualizado.

**Hotfix do iOS TVSDK 3.8.0.83**

A correção tinha o certificado de transporte de individualização atualizado.

**iOS TVSDK 3.8**

Conformidade com o iOS 13 e iOS 13 manipulada `UIWebView` Descontinuação da API.

**iOS TVSDK 3.7**

Correção de um cenário em que a reprodução era interrompida quando muitas solicitações de resolução de anúncio eram feitas simultaneamente.

**iOS TVSDK 3.6**

**Correções na propriedade de vastoXML da classe`PTNetworkAdInfo`**

A variável `vastXML` a propriedade não estava sendo definida corretamente e retornava um valor nil.

**iOS TVSDK 3.5**

**Habilitar áudio de fundo**

*Configure seu aplicativo para continuar reproduzindo áudio quando ele for colocado em segundo plano.*

Para habilitar esse recurso, devemos definir a nova API `audioPlaybackInBackground` adicionado no `PTMediaPlayer` classe. Com essa API ativada, seu aplicativo está pronto para reproduzir o áudio em segundo plano.

**iOS TVSDK 3.4.0.19 (Hotfix)**

Esta versão tem uma correção para falhas de aplicativo que ocorrem em um cenário de failover de anúncio.

**iOS TVSDK 3.4**

**Tempo limite da resolução do anúncio**

* Com o TVSDK 3.4, os usuários agora podem definir o valor de tempo limite para a resolução geral do anúncio e downloads de manifesto. Se, dentro de um determinado tempo limite, alguns anúncios não forem resolvidos, o TVSDK reproduzirá os anúncios restantes.

* `PTAdMetadata: adRequestTimeout` A API foi substituída e será removida. O valor padrão foi definido como 35 segundos.

* Duas novas APIs alternativas foram introduzidas no `PTAdMetadataClass: adResolutionTimeout`  - tempo limite para chamadas gerais de resolução de anúncio adManifestTimeout - tempo limite para downloads de manifesto de anúncio.

**Otimização da receita**

Ativação do TVSDK para identificar áreas problemáticas relacionadas a fluxos de trabalho de inserção de anúncios para relatar a um ponto de extremidade de escolha do Analytics.

**Versão 3.3**

O TVSDK 3.3 agora é compatível com o SDK 11 da iOS. Todas as APIs obsoletas foram substituídas por alternativas adequadas.

**Versão 3.2**

**Suporte adicional para registro (Fase 2)**

Adição de suporte para notificações de erro, no caso de:

* A versão HLS do anúncio usa um nível superior ao conteúdo.

* A variante somente de áudio foi excluída.

* Falha na solicitação VAST/VMAP.

**Versão 3.1**

* **Suporte adicional para registro**
Adição de suporte para notificações descritivas se houver falhas na reprodução do anúncio.

* **Adicionado [!DNL Fairplay] Suporte a fluxo CMAF criptografado**
   [!DNL Fairplay] Fluxos CMAF criptografados com reprodução de codec AVC agora são suportados.

**Versão 3.0.1**

Nenhum recurso novo ou aprimoramento nesta versão.

**Versão 3.0**

* O TVSDK 3.0 é compatível com fluxos HEVC.

* Just In Time - Resolve anúncios mais próximos a marcadores de anúncios.

Adicionado `enableDelayAdLoading` propriedade do tipo booleano na interface do nível do aplicativo para ativar a JIT. Se `enableDelayAdLoading` é NÃO, será `setadMetadata.delayAdLoading`to True (propriedade da interface PTAdMetadata).

Com essa propriedade ativada, o TVSDK resolve cada ad break antes de sua posição, com base no valor de tolerância definido. Por padrão, `delayAdTolerance` é definido como cinco segundos.

**Versão 1.4.45**

Para estar em conformidade com o Xcode10, o TVSDK mudou da `libstdc++` para `libc++`e, como resultado, a versão mínima compatível é a iOS 7. Anteriormente era o iOS 6.

**Versão 1.4.44**

Nenhum recurso novo ou aprimoramento nesta versão.

**Versão 1.4.43**

* Experiência semelhante à de TV ao poder se associar no meio de um anúncio sem acionar o rastreamento de anúncios parciais.\
   Exemplo: o usuário se junta ao meio (a 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. São 10 segundos do segundo anúncio no intervalo.

   * O segundo anúncio é reproduzido pelo tempo restante (20 segundos) seguido pelo terceiro anúncio.
   * Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente para o terceiro anúncio são acionados.

* Adicionado `enableVodPreroll` propriedade do tipo booleano na interface PTAdMetadata. A propriedade pode ser usada para ativar o pré-lançamento em um fluxo de VoD. Se `enableVodPreroll` for NÃO, o PSDK não será reproduzido antes da exibição. Isso, no entanto, não afeta os rolos intermediários. O valor padrão de `enableVodPreroll` é SIM.
* `closedCaptionDisplayEnabled` API de `PTMediaPlayer` A interface está marcada como obsoleta do iOS v1.4.43 em diante. Para determinar se as legendas ocultas estão disponíveis para um determinado `PTMediaPlayerItem`, examinar a `subtitlesOptions` propriedade de `PTMediaPlayerMediaItem`.

**Versão 1.4.42**

Nenhum recurso novo foi adicionado nesta versão. Para obter uma lista dos problemas corrigidos, consulte [Problemas resolvidos](#resolved-issues).

**Versão 1.4.41**

Alterações na API:

* **isSecure**: Uma nova API é introduzida no isSecure para proteger o reprodutor contra gravação e emissão de um erro. O valor padrão é true.

* **allowExternalRecording**: uma nova API é introduzida para permitir o espelhamento de reprodução automática para um conteúdo seguro. O espelhamento em airplay é tratado como gravação, portanto `allowExternalRecording` O valor deve ser definido como `True`, para permitir o espelhamento do airplay ou definir como `False` para interromper o espelhamento do airplay para proteger o conteúdo. Por padrão, `value` é verdadeiro.

**Versão 1.4.40**

Sem novos recursos.

**Versão 1.4.39**

* O iOS TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.

* O iOS TVSDK foi atualizado para fazer solicitações do CRS do novo host do Akamai `primetime-a.akamaihd.net`.

* A nova configuração do nome de host fornece a entrega de ativos CRS por HTTP e HTTPS (SSL) em maior escala.

**Versão 1.4.36**

Integrar e certificar o VHL 2.0 no TVSDK do iOS: reduza a barreira no `VideoHeartbeatsLibrary` redução da complexidade das APIs.

**Versão 1.4.34**

**Informações sobre Anúncios de Rede**

As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. A ID do anúncio, o Sistema de publicidade e as Extensões de anúncios VAST são fornecidos em `PTNetworkAdInfo` classe acessível por meio de  `networkAdInfo`  em um ativo de anúncio. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como **Análise do Mat**.

**Versão 1.4.31**

* **Métricas de cobrança** Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.

   Toda vez que o TVSDK gera um evento de início de fluxo, o reprodutor começa a enviar mensagens HTTP periodicamente para o sistema de cobrança do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

* **Suporte a várias CDNs para anúncios CRS** O TVSDK agora é compatível com vários CDNs para anúncios CRS. Ao fornecer detalhes de FTP para anúncios CRS, é possível especificar locais de CDN, diferentes do CDN de propriedade de Adobe padrão, como [!DNL Akamai].

**Versão 1.4.29**

No `PTSDKConfig` classe, a variável `forceHTTPS` API adicionada.

A variável `PTSDKConfig` A classe fornece métodos para impor o SSL em solicitações feitas aos servidores do Adobe Primetime Ad Decisioning, DRM e Video Analytics. Para obter mais informações, consulte `forceHTTPS` e `isForcingHTTPS` nesta classe. Se um manifesto for carregado por HTTPS, o TVSDK preservará o uso de conteúdo do HTTPS e respeitará esse uso ao carregar qualquer URL relativo desse manifesto.

>[!NOTE]
>
>As solicitações para domínios de terceiros, como pixels de rastreamento de anúncios, URLs de conteúdo e anúncios e solicitações semelhantes, não são modificadas e é responsabilidade dos provedores de conteúdo e servidores de anúncios fornecer URLs compatíveis por meio de HTTPS.

**Versão 1.4.18**

O Primetime iOS TVSDK agora é compatível com criações JavaScript VPAID 2.0 para permitir uma experiência avançada de anúncios interativos em fluxo. Para obter mais informações sobre o VPAID 2.0, consulte Suporte a anúncios VPAID.

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
   * Banners de anúncios
   * Linguagem de Marcação da TV (TVML)

**Versão 1.4.13**

>[!NOTE]
>
>O módulo Nielsen foi removido do build do TVSDK. O TVSDK será atualizado em breve com um novo módulo de integração Nielsen.

**Fallback de anúncios, encadeamento de Daisy na lógica de seleção de anúncios (Zendesk #3103)**

Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback. Para obter mais informações, consulte Fallback de anúncios para anúncios VAST e VMAP.

**Versão 1.4.9**

**Sinalização De Blecaute Com Substituição De Conteúdo Alternativo**

Como parte da atualização 1.4 do TVSDK, o Adobe agora também oferece suporte para entrada e retorno de blecautes regionais em relação ao conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando a programação alternativa estiver sendo mostrada no lugar da programação original.

**Versão 1.4.8**

**Biblioteca de Video Heartbeats (VHL) atualizada para a versão 1.5**

* Capacidade de enviar metadados com início de vídeo ou início de vídeo/anúncio/capítulo como dados de contexto.

* Menos tráfego de rede - As pulsações são menores em média e menores em tamanho.

**Versão 1.4.7**

* **Suporte à individualização no local**

Suporte para instalações locais do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para ir para um endpoint diferente.

* **Proteção de saída baseada em resolução**

As Políticas DRM agora podem especificar a maior resolução permitida, dependendo dos recursos de Proteção de saída do dispositivo. Por exemplo, _Se o HDCP estiver disponível, permita que o conteúdo com resolução de até 1080p seja reproduzido e, se o HDCP não estiver disponível, permita que o conteúdo com resolução de até 480p seja reproduzido._

**Versão 1.4.4**

* **Atualização da Biblioteca de vídeo Heartbeats (VHL) para a versão 1.4.1.1**

   * Adição da capacidade de reunir diferentes casos de uso de análise, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção do `trackAdBreakStart` e `trackAdBreakComplete` métodos. O ad break é inferido do parâmetro `trackAdStart` e `trackAdComplete` chamadas de método.
   * A variável `playhead` A propriedade não é mais necessária ao rastrear anúncios.
   * Adição de suporte para o Serviço de ID de Experience Cloud.

* **Integração do SDK Nielsen**

O TVSDK agora oferece suporte ao envio de beacons mTVR e MDPR ID3 para o SDK Nielsen, sem qualquer integração personalizada. Para começar, baixe o SDK de aplicativo 3.1.2.19 Nielsen iOS e siga as instruções encontradas aqui no Guia dos programadores do iOS.

**Versão 1.4.0**

* **Sinalização De Blecaute Com Substituição De Conteúdo Alternativo**

Como parte da atualização do TVSDK 1.4, o TVSDK também oferece suporte à entrada e ao retorno de blecautes regionais em relação ao conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando a programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remova/substitua anúncios C3**

Agora, nenhum trabalho preparatório adicional é necessário para inserir dinamicamente novos anúncios nos ativos de vídeo sob demanda (VOD) que saem da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova e poderosa funcionalidade também é útil nos casos em que o conteúdo ao vivo/linear é transmitido e é imediatamente desativado para uso como conteúdo sob demanda sem o tempo adequado para limpar o ativo.

## Problemas resolvidos {#resolved-issues}

Quando a resolução está associada a um problema relatado, uma referência do Zendesk é exibida, por exemplo, ZD#xxxxx.

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.13**

* (ZD 42085) - Problemas com a reprodução em fluxos CMAF.

* (ZD-43215) - Falha ao descartar o reprodutor enquanto um anúncio estava em andamento.

* (ZD 43210) - A reprodução do iOS HLS congela quando a legenda WebVTT está ativada.

**iOS TVSDK 3.12**

* O fluxo ao vivo falha após 15 minutos de reprodução ao usar o TVSDK para iOS 3.10.

### Problemas resolvidos nas versões anteriores {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - O `isFallbackOnInvalidCreativeEnabled` causa falha no aplicativo.

* (ZD#41289) - `NSInvalidArgumentException` é observado com o método `customParams` levando à falha do aplicativo.

**iOS TVSDK 3.10**

(ZD#40943) - O reprodutor TVSDK não é acionado `PTMediaPlayerStatusError` notificação quando a rede não estiver disponível.

**iOS TVSDK 3.9**

(ZD#40272) - O iOS TVSDK falha ao reproduzir legendas em VTT com o erro 101001 e leva ao congelamento do aplicativo.

**iOS TVSDK 3.8**

* (ZD#40087) - O iOS trava com um erro do player para conteúdo de VOD expirado.

* (ZD#40083) - Os anúncios precedentes não são exibidos para transmissão em tempo real com `OpportunityGenerator` O e o reprodutor informam o erro.

* (ZD#39828) - `CurrentItem` A propriedade não tem a anotação de nulidade, causando falha do player quando o status do player contido na notificação é `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) - O conteúdo falha ao ser reproduzido na janela Picture-in-Picture (PiP) depois que um conteúdo conclui a reprodução, quando vários conteúdos são configurados para serem reproduzidos na PiP.

**iOS TVSDK 3.6**

Nenhum problema novo nesta versão.

**iOS TVSDK 3.5**

Nenhum problema novo nesta versão.

**Versão 3.3**

(ZD#37820) - Adição de uma lista de permissões para cabeçalho personalizado HS-Id, HS-SSAI-TAG.

**Versão 3.2**

* **Ingresso nº 36588** - Uma falha no reprodutor é observada quando o método STOP do MediaPlayer é chamado.

Correção de uma falha intermitente observada quando o método STOP é chamado para alguns fluxos com legendas.

* **Tíquete nº 37080** - Solicitações duplicadas vistas para chamadas Manifest.
Correção das solicitações duplicadas feitas para URLs de Manifesto durante a reprodução. O TVSDK agora faz uma chamada por manifesto.

* **Tíquete nº 37** - Falha na regra de normalização CRS com tipo de correspondência eq Correção de um caso em que o reprodutor falhava quando encontrado com a última regra de normalização definida para nomes de host com um tipo de correspondência &quot;eq&quot;.

**Versão 3.1**

**Tíquete #36313** - Resultados intermitentes e imprevisíveis durante interrupções de anúncios lineares Corrigida a reprodução intermitente durante interrupções de anúncios lineares no fluxo ao vivo.

**Versão 3.0.1**

**Ingresso36948** - CRS - Ordem de seleção de ativos inconsistente no iOS 12 O ativo selecionado para CRS nem sempre é a variante de mais alta qualidade retornada em uma resposta VAST ou VMAP.

**Versão 3.0**

* **Ingresso35311** - O status do player não é PAUSADO durante uma interrupção de chamada telefônica Adicionado manipulador de interrupção para impedir a interrupção do player. Ao interromper, o status do reprodutor fica PAUSADO e, em seguida, reinicia a reprodução ao clicar no botão Reproduzir.

* **Tíquete36685** - Ativos ao vivo - Incompatibilidade de tempo com o progresso do tempo do player e o tempo do marcador SCTE O tempo correto é calculado para os marcadores SCTE que estão à frente do ponto ao vivo.

* **Tíquete36492** - `currentTime` e `localTime` não é atualizado ao procurar uma nova posição durante o status pausado A hora atual do player agora pode ser definida como zero caso o player esteja no estado pausado; anteriormente, a hora atual costumava ser definida como zero somente no estado de reprodução.

**Versão 1.4.45**

* **Tíquete36294** - iOS TVSDK não funcional com Xcode 10 Corrigidos os problemas de compilação com TVSDK no XCode 10. Devido aos requisitos do XCode 10, os aplicativos criados no TVSDK para iOS a partir da versão 1.4.45 exigem o direcionamento mínimo de implantação como o iOS 7.0

* **Tíquete36321** - Discrepância observada no intervalo buscável entre `PTMediaPlayer` e `AVPlayer` instância em _Reproduzindo_ estado.

* **Ingresso36493** - `libstdc++` suporte no iOS 12 Correção de problemas de compilação com o TVSDK no iOS 12. Os aplicativos criados com o TVSDK para iOS 1.4.45 em diante exigem o direcionamento mínimo de implantação como o iOS 7.0

**Versão 1.4.44**

* **Ingresso34683** - O Tempo De Progresso Da Reprodução Do Anúncio Está Indo Negativo

Verificações adicionais são colocadas para lidar com o caso quando há uma incompatibilidade entre a duração relatada pelo servidor de publicidade e o conteúdo real do anúncio.

* **Tíquete34801** - `currentTime` e `localTime` não eram atualizados ao procurar uma nova posição durante o status pausado A hora atual do player agora pode ser definida como zero caso o player esteja no estado pausado; anteriormente, a hora atual costumava ser definida como zero somente no estado de reprodução.

* **Tíquete35037** - A reprodução pára com um URL inválido ao retornar da inserção de anúncio baseada em sinal.
Correção aprimorada fornecida para o problema fechado #34385 na versão 1.4.42. Adição do código de controle de verificação e exceção isCancelled para tornar a fila de operações mais robusta.

**Versão 1.4.43**

* (ZD#32990) - iOS: reprodução de conteúdo em vez de anúncios em alguns pontos de sinalização. `selectedMediaOptionInMediaSelectionGroup` A API que fazia parte da interface AVPlayerItem agora foi movida para `AVMediaSelection` no iOS 11. O problema foi resolvido usando essa nova API.

* (ZD#33683) TVSDK removido `==` sufixo das cadeias de caracteres de metadados. O problema é corrigido na lógica de análise.

* (ZD#33905) - iOS TVSDK que faz chamadas para os arquivos manifest com dois agentes do usuário. O problema do agente do usuário foi corrigido na primeira chamada m3u8 (novo caso de instalação). As M3u8 têm os mesmos user-agents para todas as chamadas agora.

* (ZD#34293) - Os pré-rolagens inseridos em fluxos LINEARES não são reproduzidos corretamente no iOS11. O problema é corrigido para anúncios antes da exibição.

* (ZD#34684) - Quando a política de ignorar anúncio é aplicada, os quadros de anúncio precedentes são exibidos por alguns segundos. Uma nova API, `enableVodPreroll` foi introduzido para desativar a reprodução antes da exibição na reprodução de vod. O valor padrão para essa API é _Sim_. A API garante que a compilação de conteúdo de anúncios seja ignorada no conteúdo principal.

* (ZD#34765) - Depois de chamar `stop()`, alguns segmentos de Fluxos de transporte ainda são baixados. Aprimoramento do `Stop()` API para evitar o download de segmentos extras.

* (ZD#34865) - Anúncios antes da exibição para [!DNL Livestream] são truncados no iOS. Relacionado ao iOS11, e adicionar uma verificação extra para confirmar se o fluxo é pré-lançamento ou conteúdo principal resolve esse problema.

* (ZD#35093) - Corrigido um cenário de failover em que, se a variante principal do fluxo falhar na inicialização (retorna 404), a reprodução não alternará para o fluxo de backup.

**1.4.42 (1.4.42.118)**

* (ZD#34385) - A reprodução é interrompida com um URL inválido ao retornar da inserção de anúncio baseada em sinal.

   Aumentar as contagens simultâneas máximas para `CustomAVAssetLoaderOperations`, para que as leituras do manifesto possam continuar a ser executadas.

* (ZD#34373) - Os usuários finais não podem fazer streaming para dispositivos conectados a HDMI, quando a gravação de stream não é permitida.

* (ZD#32678) - O TVSDK não coleta as IDs de anúncios corretas no iOS.

   A ID do anúncio final do criativo agora é selecionada nos pings do VHL se houver redirecionamentos VAST/VMAP.

* (ZD#33904) - O TVSDK não está registrado para notificações do AVFfoundation `AVAudioSessionMediaServicesWereLostNotification` e `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` e `PTMediaServicesWereResetNotification` O agora pode ser registrado no aplicativo do player para receber as notificações quando os serviços de mídia são redefinidos ou perdidos.

* (ZD#33815) - Os clientes não conseguem atualizar suas regras de priorização e normalização do CRS sem exigir uma atualização do aplicativo.

   Adição de `getCRSRulesJsonURL` e `setCRSRulesJsonURL` APIs para o iOS TVSDK.

**Versão 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemas de criação do aplicativo de referência com o TVSDK versão 1.4.41

   A partir desta versão, o Xcode 9 é necessário para compilar o TVSDK para iOS.
* (ZD #29456) - Início da reprodução no estado pausado

   Correção do problema de pausa que ocorre quando o vídeo é pausado ao entrar na reprodução.
* (ZD #30371) - A hora de início do AdBreak muda quando inserimos mais de dois anúncios em fluxo linear

   Correção do erro ao tentar reproduzir conteúdo na Apple TV, o que impede a reprodução completamente
* (ZD #32146)- Não `PTMediaPlayerStatusError` é recebido para conteúdo HLS Live no bloqueio do iOS 11 dev beta

   Não `PTMediaPlayerStatusError` O é recebido para conteúdo HLS Live e VOD no bloqueio usando o Charles (Drop connection e 403).

* (ZD #29242) - A reprodução do vídeo Airplay falha com os anúncios ativados.

   Quando os anúncios estão ativados e o AirPlay está ativado ao iniciar a reprodução de um vídeo, a reprodução nunca é iniciada e nenhum erro é exibido.

* (ZD#33341) - `DRMInterface.h` aciona avisos de criação no Xcode 9.

   Correção de dois protótipos de bloco no `DRMInterface.h` que não tinham a palavra &#39;void&#39; em suas listas de parâmetros.

* (ZD#31979) - Não compila/executa quando é iOS 10 ou posterior para iPhone 7/iPhone7+.

   A compilação fixa de documentos IB para versões anteriores ao iOS 7 não é mais suportada.

* (ZD#32920) - Tela em branco dentro de um Ad break e sem conclusão de Ad break.

   Quando um Ad break está apresentando Instâncias de anúncio e após a conclusão de uma instância de anúncio, uma tela em branco é exibida.

* (ZD#32509) - Desative o iOS 11 screen recoding Desative a gravação de tela no iOS 11.

* (ZD#33179) - Falha intermitente de evento no iOS11.

   Correção da falha de evento no iOS 11.

**Versão 1.4.40** (1.4.40.72)

* (ZD #32465) - O player não pode manipular listas de reprodução mescladas.

   Chame `finishLoadingWithError`(with: Error) para que o AV Foundation tente fluxos alternativos/failover de acionador.

* (ZD #31951) - Erro de TVSDK durante rotações de licença.

   Correção do problema de rotação de licenças.
* (ZD #31951) - Tela em branco dentro de um Ad break e sem conclusão de Ad break.

   Lidou com um problema em que os anúncios VPAID do Facebook frequentemente retornavam vários blocos CDATA em um único `<AdParameters>` Nó VAST.
* (ZD #33336) - iOS TVSDK - Os pods de anúncios não estão sendo preenchidos, apesar de anúncios suficientes serem retornados pelo Freewheel.

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

* (ZD #29176) - Falha em `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

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

O problema foi corrigido. O TVSDK da iOS está acionando um `exception(AUDNetworkAdInfo::initWithAdId)` e não lidar com isso. A exceção se deve à ID vazia do anúncio.

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

* (ZD #28481) - Interrupção do FER devido à anexação da chave incorreta ao final de um ad break para esses fluxos de FER

Para um fluxo FER, a chave antes do ad break é inserida após o fim do ad break. Esse problema foi resolvido anexando o *última chave vista* no fim do ad break.

**Versão 1.4.33** (1.4.33.803 para iOS 6.0+)

* (ZD# 21701) Habilitar CRS para Subcontas

Ativado ao enviar o URL criativo original para a solicitação do CRS 1401 em vez do URL normalizado, de acordo com o requisito para o back-end do CRS.

* (ZD# 26218) - `PSDKResources.bundle` carregando problema

Esse problema foi resolvido atualizando o carregamento de recursos para procurar em todos os pacotes disponíveis.

* (ZD# 27460) Primeira chamada de anúncio Midroll - POST para `cdn.auditude.com` retornando 403.

A nova conta CDN não pode lidar com uma solicitação CDN POST. Esse problema foi resolvido atualizando o código para fazer o `cdn.auditude.com` solicitação de anúncio para ser GET em vez de POST.

**Versão 1.4.32** (1.4.32.792 para iOS 6.0+)

* (ZD# 27132) Suporte para valores decimais para quebras de anúncios VMAP.

Quando o conteúdo não era segmentado ao longo dos ad breaks definidos, os números inteiros estavam causando posicionamentos de anúncios inesperados. O problema foi resolvido sem converter os valores decimais em números inteiros.

* (ZD# 27189) O conteúdo AES com a tag EXT-X-DISCONTINUITY-SEQUENCE não está sendo reproduzido corretamente.

O problema foi resolvido colocando a tag no início da lista de reprodução.

**Versão 1.4.31** (1.4.31.785 para iOS 6.0+)

* (ZD# 24528) Implementar Métricas de Uso do TVSDK para Faturamento

Para obter mais informações, consulte [Métricas de cobrança].

* (ZD# 24642) Suporte Picture-in-Picture para TVSDK

O recurso picture-in-picture, que às vezes não funcionava corretamente, foi corrigido.

* (ZD# 25246) Sinais De Ad Break Incorretos

Esse problema foi resolvido alinhando tags de descontinuidade em manifestos de variante.

* (ZD# 26218) O processo de compilação do aplicativo fica complicado ao tentar incluir `PSDKLibrary.framework` na estrutura do aplicativo do cliente

Esse problema foi resolvido empacotando o `PSDKLibrary.framework` conforme solicitado.

* (ZD# 26364) Suporte a vários CDNs para anúncios CRS

Para obter mais informações, consulte Suporte a vários CDNs para entrega de anúncios CRS.

* (ZD# 27028) Atraso na reprodução de alguns fluxos no iOS 10.

Esse problema foi resolvido fornecendo uma solução alternativa para fluxos que não têm uma extensão M3U8.

**Versão 1.4.30** (1.4.30.754 para iOS 6.0+)

Os seguintes problemas foram resolvidos para TVSDK nesta versão:

* (ZD# 24180) Adicione um cabeçalho personalizado ao incluo na lista de permissões.

Um novo cabeçalho personalizado foi adicionado ao incluo na lista de permissões TVSDK.

* (ZD# 25016) O fluxo de failover é selecionado aleatoriamente quando os parâmetros de controle ABR são definidos

Esse problema foi resolvido mantendo os fluxos ABR em ordem quando as configurações ABR são fornecidas com o `initialBitrate` em um fluxo que inclui URLs de failover. Isso evita a reprodução dos fluxos de failover em vez do principal.

* (ZD# 25076) Falha em `PTAuditudeAdResolver loadComplete`

O problema em que uma falha ocorria durante o início/término rápido de várias instâncias do PTMediaPlayer com anúncios foi corrigido.

* (ZD# 25960) Nenhuma tag adicional assinada está acionando difusões de notificação de alteração de metadados

O problema em que uma tag assinada não é notificada quando aparece antes que o primeiro segmento no manifesto tenha sido corrigido.

* (ZD# 26084) PSDK lançando um 106000.101000.Erro -11833 decodificador não encontrado ao fazer a transição do último ad break para conteúdo de entretenimento

Quando o último tempo de início de ad break do VMAP cai antes da duração total ser concluída, em determinadas condições, a chave não é inserida até o final do último ad break. Esse problema foi corrigido.

* A Biblioteca do Video Heartbeat (VHL) foi atualizada para a versão 1.5.9 para resolver os seguintes problemas:

* (ZD #22351) VHL - Analytics: duração do ativo de vídeo ao vivo

Esse problema foi resolvido adicionando o  `assetDuration`  API para `PTVideoAnalyticsTrackingMetadata` para atualizar a duração do ativo para fluxos ao vivo/lineares e fornecer uma lógica para verificar o fluxo ao vivo.

* (ZD# 22675) VHL - Analytics: atualização da duração do ativo de vídeo ao vivo

Este problema é o mesmo que ZD #22351.

* (ZD #25908) VHL - Analytics: Falha no evento do Adobe Heartbeat

Esse problema foi resolvido com a atualização da implementação para usar a versão mais recente do VHL para iOS versão 1.5.9 para melhorar a estabilidade e o desempenho.

* (ZD #25956) VHL - Analytics: falha ao reproduzir vídeos repetidamente

Este problema é o mesmo que ZD #25908.

**Versão 1.4.29** (1.4.29.743)

* (ZD# 23901) Anúncios de terceiros não estão sendo exibidos

Esse problema foi resolvido movendo-se para a estrutura de URL do CRS v3 para incluir a ID da região no URL reempacotado.

* (ZD #25183) Problemas com a reprodução DRM no tvOS e no iOS

Esse problema foi resolvido fornecendo suporte para várias tags principais necessárias para suporte a vários DRMs.

* (ZD# 25334) Falha do TVSDK ao reproduzir um conteúdo compartilhado cDVR

Esse problema era resolvido evitando que o TVSDK convertesse cadeias de caracteres vazias em URLs absolutas.

* (ZD# 25347) Definir cabeçalho HTTP personalizado no AVURLAsset

Suporte para cabeçalhos personalizados em solicitações de segmento ts por meio da `PTNetworkConfiguration` A classe foi adicionada.

**Versão 1.4.28** (1.4.28.722)

* (ZD #24549) Várias chamadas de rastreamento de anúncios

Esse problema foi resolvido atualizando o gerenciador de linha do tempo para acompanhar as notificações em um objeto específico quando vários players são criados.

* (ZD #24758) `PTManifestLogger` não é compatível com o iOS 8

Esse problema foi resolvido atualizando a biblioteca do utilitário logger para o destino de implantação da versão 7.0.

* (ZD #24775) Fluxo atrasado devido a Anúncios

Esse problema foi resolvido calculando corretamente a variação de duração nas listas de reprodução do evento.

* (ZD #24799) Alguns episódios não estão sendo reproduzidos no iOS APP

Esse problema era resolvido usando o servidor Web local para legendas quando os arquivos WebVTT eram geo-restritos.

**Versão 1.4.27** (1.4.27.711) para iOS 6.0+

* (ZD #24089) - Otimizações para resolução de anúncios em fluxos DVR longos

Esse problema foi resolvido adicionando várias otimizações para reduzir o tempo necessário para processar a janela do DVR em fluxos ao vivo/lineares.

* (ZD #21554) - Os beacons de erro do TVSDK não são acionados para `application-type = video/mp4`

Esse problema foi resolvido permitindo que o reprodutor execute ping nos URLs de rastreamento de erros corretos em formatos de ativos inválidos.

* (ZD #24424) - Falha de tipo `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` é originária de dentro `PSDKLib` para iOS em dispositivos de hardware mais recentes.

A falha que ocorria devido a uma instância de reprodutor de mídia desalocada, quando a reprodução é alternada rapidamente entre fluxos diferentes, foi corrigida.

* (ZD #24575) - Falha no TVSDK em dispositivos de 32 bits quando `enableDebugLog=true`

O problema no formato de log que causava a falha em dispositivos de 32 bits quando o registro era ativado foi corrigido.

**Versão 1.4.26** (1.4.26.702) para iOS 6.0+

* (ZD# 20213) - O FW TVSDK deve ser dinâmico/modularizado para XCode7

Corrigido ao atualizar as bibliotecas com suporte ao módulo

**Versão 1.4.25** (1.4.25.684) para iOS 6.0+

* (ZD #19629) - Pausa de vídeo ao vivo ao entrar no Airplay para ATV 4

Esse problema foi resolvido adicionando um período de espera após a remoção de itens antigos, mas antes de adicionar novos itens à `AVQueuePlayer`. Sem o período de espera, as notificações são enviadas ao item incorreto.

* (ZD #19856) - Nenhuma legenda é exibida quando habilitada por padrão

Os problemas na lista de reprodução de webvtt, que fazia com que as legendas não fossem exibidas corretamente, foram corrigidos.

* (ZD #21590) - Desempenho e rastreamento de vídeo nas compilações de origem mais recentes

O problema sobre a duração do vídeo ausente no `VideoAnalytics` foi corrigido.

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

Esse problema foi resolvido atualizando a lógica para reexibir a visualização do player se um anúncio VPAID não for reproduzido.

* (ZD #20101) - A implementação de capítulo personalizado aciona o evento de início de capítulo durante a reprodução de anúncio

Esse problema foi resolvido com a atualização `VideoAnalyticsTracker` para detectar corretamente o início/término do capítulo ao fazer a transição entre limites de capítulo e não capítulos.

* (ZD #20784) - Analytics: o acionamento de conclusões de conteúdo para transições de vídeo ao vivo

Esse problema foi resolvido adicionando uma lógica para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo.

As seguintes bibliotecas foram atualizadas:

* Biblioteca do AdobeMobile para 4.10.0
* Biblioteca do VHL para 1.5.6
* Biblioteca VHL-Nielsen para 1.6.7
* (ZD #21855) - As legendas não são reproduzidas após o lançamento

Nesse problema, as tags de descontinuidade duplicadas faziam com que as legendas não aparecessem depois do meio da exibição. Esse problema foi resolvido removendo as tags de descontinuidade que estão próximas umas das outras.

* (ZD #21994) - String fora dos limites em `PTHLSUtils`

A causa mais provável da falha é quando uma EXT-X-KEY tem um URL entre aspas.

* ZD #22074) - `AUDVAST` Falha ocorre uma vez por minuto no iOS

Na versão 1.4.23, a falha causada pela presença de caracteres inseguros em um URL de redirecionamento VAST foi corrigida. No entanto, o TVSDK continuava ignorando esses anúncios.

Esse problema foi resolvido ao manipular os caracteres inseguros e permitir que os anúncios fossem reproduzidos.

* (ZD #22694) - `PTMediaPlayer`.  A visualização está oculta pelo reprodutor

Esse problema foi resolvido atualizando a lógica para reexibir a visualização do player se um anúncio VPAID não for reproduzido.

**Versão 1.4.23** (1.4.23.641) para iOS 6.0+

* (ZD #18016) - Nenhuma resposta do SDK do Primetime com uma condição de rede incorreta

Esse problema foi resolvido melhorando a notificação de erros quando um erro fatal de `AVFoundation` ocorre e para permitir que o aplicativo manipule a reinicialização após o erro.

* (ZD #20580) - Falha no `PTSplicerManager`

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

As APIs foram adicionadas à `PTNetworkConfiguration` classe para anexar cookies como parâmetros de URL em segmentos para determinados fluxos tokenizados do Akamai.

* (ZD #21287) - Log Irrelevante

Um problema com algumas instruções de log mostradas por padrão no console xcode, mesmo quando o registro está desativado, foi corrigido.

* (ZD #21446) - Eventos de ad break às vezes não acionados pelo TVSDK

Nos fluxos de EVENTO, as ad breaks não são acionados corretamente na build da versão anterior. Esta build aborda esse problema.

**Versão 1.4.21** (1.4.21.605) para iOS 6.0+

* (ZD #20749) - O fallback ignora respostas VAST não vazias; URLs de rastreamento de anúncios extras são acionados

Um problema com pings duplicados em anúncios de fallback foi resolvido.

**Versão 1.4.20** (1.4.20.590) para iOS 6.0+

* (ZD #18639) - O TVSDK está usando CPU/recursos em excesso em um ativo de gravação lenta

O uso excessivo de CPU/recursos foi corrigido nos dois níveis. Primeiro, permitindo que a função de atualização de tempo seja executada em uma fila global, em vez da thread principal, e otimizando o uso da CPU para analisar o manifesto com o m3u8 processado e armazenado em cache anteriormente.

* (ZD #19349) - Os anúncios precedentes estão sendo ignorados ao limitar a conexão de rede.

Esse problema foi resolvido fornecendo um evento de tempo limite (requestTimeout) ao aplicativo e ao `adMetadata.adRequestTimeout` API para substituir o tempo limite padrão de 10 segundos.

* (ZD #19446) - Notificação ausente em fluxos ao vivo

Esse problema foi resolvido permitindo que o aplicativo assinasse o `EXT-X-PROGRAM-DATE-TIME` em transmissões ao vivo.

* (ZD #19459) - Falha ao preparar áudio alternativo com `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) - Falha - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

Esta edição é a mesma do Zendesk #19459.

* (ZD #19574) - O TVSDK não está retornando dados de resposta do M3U8 para conteúdo DRM ou não DRM

No carregamento inicial do arquivo de manifesto em `PTMediaPlayerItem.prepareToPlay`, se o carregamento do manifesto falhar, o TVSDK não relatará o corpo da resposta de falha ao aplicativo.

Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro ao aplicativo.

* (ZD #19615) - A lógica de fallback não está funcionando

Na implementação atual, os anúncios de fallback foram ignorados e não foram empacotados novamente, a menos que esses anúncios estejam no formato m3u8. Esse problema foi resolvido adicionando também o suporte ao reempacotamento de anúncios de fallback.

* (ZD #19770) - O TVSDK não reproduz nenhum conteúdo AES protegido com redirecionamento 302

O problema de redirecionamento foi corrigido porque o URL de redirecionamento estava sendo apagado pelo `cleanConnectionData` antes que pudesse ser usado para analisar o manifesto.

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

* (ZD#18956) - `player.drmManager` é nil quando o ponto de interrupção é definido no reprodutor de demonstração do iOS

Esse problema foi resolvido atualizando o `PTMediaPlayer.drmManager` Implementação da API para coletar o DRManager da estrutura do DRM.

**Versão 1.4.18** ( 1.4.18.557) para iOS 6.0+

* (ZD #18844) Rastreamento do indicador de reprodução do conteúdo ao vivo no iOS player.

Esse problema foi resolvido permitindo que os aplicativos definissem seu próprio valor de indicador de reprodução.

* (Zendesk #18518) - Se o nome do vídeo não for especificado, o nome do TVSDK assumirá como padrão * reprodutor baseado em PSDK.*

Esse problema foi resolvido com a remoção do valor padrão para o nome do reprodutor.

**Versão 1.4.17** (1.4.17.545) para iOS 6.0+

* (Zendesk #2228) - Aprimore o TVSDK para retornar a resposta JSON da busca de um manifesto

Em vez de enviar um erro quando o conteúdo não é M3U8, o DRM Framework retorna um DRMetadata nil. O problema era resolvido adicionando metadados para expor conteúdo quando a notificação M3U8_PARSER_ERROR ocorria.

* (Zendesk #2231) - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification

Mesma resolução que Zendesk #2228

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` macro não preenchida

O problema em que a variável [!DNL Auditude] O SDK não está enviando um ping quando o URL de rastreamento tem espaços no início foram resolvidos.

* (Zendesk #17294) - Acidente [!DNL SecKeyRawSign]

Uma possível falha quando o código do cliente usa o conjunto de chaves foi resolvida.

* (Zendesk #18008) - Cookies de suporte para iOS8+ para suportar fluxos tokenizados

Fluxos tokenizados do Akamai exigem que os cookies sejam enviados em solicitações de segmento, e isso não foi possível no iOS 7 e versões anteriores. A partir do iOS 8, a Apple adicionou uma API que permite que os cookies sejam transmitidos para solicitações de segmento. Esse suporte agora está disponível no TVSDK. Também foi adicionado suporte para enviar um user-agent, se disponível.

* (Zendesk #18166) - O TVSDK 1.4.15 fornece centenas de avisos ao compilar com `DWARF` com `dSYM` opções de arquivo

Todos os avisos foram resolvidos.

**Nota**: bibliotecas compatíveis com tvOS foram adicionadas para TVSDK .

**Versão 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S Trava durante a reprodução

Revertendo a dependência de OKHTTP em [!DNL Auditude] para CRS porque o TVSDK agora está usando diretamente o `httpurlconnection` em vez de curl. O problema foi resolvido limpando as exceções antes de fazer outra chamada JNI.

* (Zendesk #4487) - Rastreamento do canal linear de conteúdo

O problema foi resolvido ao reinicializar o rastreador de heartbeat de vídeo durante uma sessão de reprodução de fluxo linear.

* (Zendesk #17919) - Android - A busca de conteúdo causa erro de heartbeat

O problema era resolver a pulsação em um estado de erro quando há uma busca em um capítulo

* (Zendesk #18053) - Aplicativo que usa o TVSDK falha em Marshmallow

O TVSDK travava no Android™ M OS quando a biblioteca TVSDK usa um código de néon que faz o YUV `->` conversão de cores de RGB. Esse problema foi resolvido atualizando as funções que estão causando esse problema usando a versão não neon do `code`.

* (Zendesk #18072) - Android M - Falha de Aplicativo

Esta falha ocorre ao chamar `MediaCodecList` e `MediaCodecInfo` APIs ao verificar se o perfil e o nível são compatíveis. A Adobe está buscando o suporte da Google para obter insights adicionais. Esse problema foi resolvido fornecendo uma solução temporária, carregando todas as informações do codec antecipadamente para evitar a chamada dessas APIs somente quando as informações do codec forem necessárias.

* (Zendesk #18074) - Legendas em árabe que não funcionam no Nexus com Android™ 6.0

Esse problema foi resolvido com o suporte ao mapa de fontes CTS do Android™.

**Versão 1.4.15** (1.4.15.512) para iOS 6.0+

**Nota**: o módulo Nielsen foi removido da build do TVSDK, mas o TVSDK será atualizado em breve com um novo módulo de integração Nielsen.

* (ZD #2228) - Erro retornado da busca do manifesto indisponível em `MediaPlayerNotification`

Adição de metadados para expor conteúdo quando a notificação `M3U8_PARSER_ERROR` ocorre.

* (ZD #4437) - Falhas dentro do SDK do Adobe Primetime

Correção de uma falha relatada ao preparar legendas/áudio alternativo.

* (ZD #4487) - Rastreamento do canal linear de conteúdo

Reinicialização permitida do rastreador de heartbeat de vídeo durante uma sessão de reprodução de fluxo linear.

**Versão 1.4.14** (1.4.14.498) para iOS 6.0+

* (ZD #17260) - Falha em `playlistManagerForURL`

Correção de uma falha intermitente devido a problemas de simultaneidade.

**Versão 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` macro não preenchida

   * O código de erro 400 é exposto se o anúncio em linha tiver criação incorreta.
   * `[ERRORCODE]` A macro é codificada por URL.

* (ZD #3865) Integração do Heartbeat com anúncios do IMA

Correção de um erro em que a duração do vídeo era relatada incorretamente.

* Atualização do reprodutor de demonstração TVSDK para oferecer suporte ao iOS 9

Para oferecer suporte adequado ao iOS 9, você deve configurar as exceções do Application Transportation Security. Para a demonstração, o ATS é completamente desativado.

**Versão 1.4.12** (1.4.12.464) para iOS 6.0+

* (ZD #4521) CRS Testando lado do cliente e SSAI

Corrigido o MD5 incorreto e reverso no URL 3P.

**Versão 1.4.12** (1.4.12.463) para iOS 6.0+

* (ZD #2751) CSAI e CRS / Enhance: lidam com elementos dinâmicos em determinados URLs de arquivo de mídia.

Serviço de reempacotamento criativo atualizado para lidar adequadamente com anúncios com URLs criativos dinâmicos.

* (ZD #3654) Vazamento de memória na versão PSDK após 1.3.4.166

Correção de vazamento de memória no `drmFramework` com reprodução regular em dispositivos iOS 8.2

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

Atualizado `PTPlaybackInformation` para expor a taxa de bits indicada atualizada. Atualizado `BITRATE_CHANGE` notificação para ser mais confiável e preciso em relação às taxas de bits relatadas do M3U8.

* (ZD #3324) Problemas de relatório de anúncios do Primetime quando nenhuma mídia de anúncio no VMAP

Suporte para ping de URLs vazios de rastreamento de ad break. O TVSDK agora verifica o início do ad break e conclui os pings de ad break vazios.

**Versão 1.4.8** (1.4.8.402)

* (ZD #3158) O IOS 7 falha em repetições completas de evento

**Versão 1.4.7** (1.4.7.382)

* (ZD #2197) Rastreamento de erros de anúncios. Adição de notificação para falha do ativo ao carregar manifesto.
* (ZD #2894) O Player faz quatro solicitações de manifesto de nível superior durante a reprodução.
* (ZD #2992) [!DNL Auditude] Relatando durações e identificadores estranhos.

**Versão 1.4.6**(1.4.6.325)

* (ZD #2197) Rastreamento de erros de anúncios. Adicionada notificação para falha do ativo ao carregar o manifesto

**Versão 1.4.5** (1.4.5.283)

* (ZD #2141) Implementação do Analytics para [!DNL TreeHouse] aplicativo, adicionado `AdobeAnalyticsPlugin.a` biblioteca para criar o pacote .
* Atualização da biblioteca de vídeo Heartbeats para 1.4.1.2
* (PTPALY-4226) (relacionado a ZD #2423) A execução da Redefinição de DRM pode resultar na exclusão dos dados do Documento de Aplicativo.

**Versão 1.4.4** (1.4.4.242)

* Atualização da Biblioteca de vídeo Heartbeats (VHL) para 1.4.1.

* (ZD #2435) Documentação do SDK da TV sobre atualizações de necessidades de análise

**Versão 1.4.2** (1.4.2.210 : iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` retornando vazio
* (ZD #2109) O Primetime PSDK 1.4.1.125 não funciona com o Xcode 5.1.1
* (ZD #2137) Falha no PSDK no iOS quando os metadados de DRM não podem ser carregados

**Versão 1.4.1**(1.4.1.125)

* (ZD #1107) [!DNL CocoaLumberjack] símbolos duplicados
* (ZD #1644) Modificar o Agente do usuário do iOS para direcionamento e relatórios
* (ZD #1850) Arquivos do Cocoa Lumberjack incluídos no SDK do iOS
* (ZD#1908) Tags personalizadas são ignoradas por PSDK se houver mais de 1

**Versão 1.4.0** (1.4.0.32)

* Zendesk #1024 - Recurso para remover anúncio de transmissão via manifesto

## Certificação e suporte do dispositivo {#device-certification-and-support}

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
* Suporte DRM para forçar HTTPS adicionando  `forceHTTPS`  e `isForcingHTTPS` APIs.
* As bibliotecas do VHL foram atualizadas para 1.5.8, as bibliotecas do Adobe Mobile foram atualizadas para 4.8.4 e a biblioteca do utilitário logger foi atualizada para a versão 7.0 do target de implantação.

**Versão 1.4.19**

Esta versão do TVSDK foi certificada com o FairPlay Support para iOS e tvOS.

**Versão 1.4.17**

* tvOS

   Esta versão do TVSDK inclui suporte para tvOS e foi certificada para fluxos HLS não criptografados.

   **Nota**: Lembre-se das seguintes diretrizes de compilação:

   * O suporte para tvOs TVSDK é limitado a fluxos criptografados não DRM de Adobe. Você deve remover a referência a `drmNativeInterface.framework` nas configurações de build do tvOS. Os fluxos criptografados AES ainda são compatíveis.
   * O Apple exige que todos os aplicativos da Apple TV sejam habilitados para código de bits, portanto, você deve ativar esse sinalizador nas configurações do projeto.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

* Devido à descontinuação da classe UIWebView do iOS, no iOS TVSDK 3.6 em diante:
   * Os anúncios VPAID não são reproduzidos conforme esperado no iPad 13.
   * Os anúncios de companhia não são reproduzidos como esperado.

* No iOS TVSDK, todos os anúncios são compilados no manifesto de conteúdo. Comportamentos de anúncios são implementados pela busca com base na duração do conteúdo e dos segmentos de anúncios. Portanto, se as durações do segmento não forem precisas, a busca nem sempre pode terminar no quadro exato do início ou do fim do ad break. Mesmo que as durações estejam relacionadas ao quadro, há uma tolerância que a própria plataforma impõe na busca e pode haver alguns quadros, anúncios ou conteúdo exibidos. Essa é uma limitação da plataforma e a maneira como a inserção de anúncios funciona com o TVSDK no iOS.
* Nesse caso, a decisão de ignorar acontece no evento de busca. No entanto, como as durações do segmento de anúncio no manifesto não representam com precisão a duração real do anúncio, a busca não tem precisão de quadro. Portanto, você verá alguns quadros de anúncios quando as políticas de anúncios forem aplicadas.
* Pode ser que o vídeo de rotação de licença não seja reproduzido no iOS 11 e funcionará bem no iOS 9.x e no iOS 10.x.
* No suporte ao VPAID 2.0, se a reprodução estiver ativa no AirPlay, os anúncios VPAID serão ignorados.
* A variável `drmNativeInterface.framework` não vincula corretamente quando o target mínimo é definido como iOS7 (ou posterior).
Solução alternativa: especifique explicitamente a `libstdc++.6.dylib` da seguinte maneira: vá para **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** e adicionar `libstdc++.6.dylib`.
* O anúncio pós-implantação não é inserido para substituir a API.
* Buscar um ad break (sem sair dele) emite uma notificação duplicada de início de anúncio e ad break
* Configuração `currentTimeUpdateInterval` não tem qualquer efeito.
Observação: em determinadas versões do iOS, o SO não carrega os recursos dentro do `PSDKLibrary.framework` automaticamente. É importante copiar manualmente a variável `PSDKResources.bundle` para os recursos do pacote do aplicativo: Vá para **Fases de criação** e copiar recursos do pacote.
* O aplicativo de referência não pode ser criado usando o Xcode 8 ou versões anteriores. iOS TVSDK versão 1.4.41 em diante, use o Xcode 9 para compilar.
* Os anúncios VPAID não respeitam o `delayAdLoadingTolerance` valor.
* 24077- Para certos conteúdos HLS com legendas, o player trava em _Parar_ ou _Redefinir_ método.
* Notificações de erro detalhadas não estão disponíveis em caso de resolução de anúncio Just in Time estar habilitada.
* As notificações de erro são registradas de acordo com o tempo de resolução do anúncio e não de acordo com a sequência de anúncios.
* O suporte a HEVC tem as seguintes limitações nesta versão
   * DRM sem suporte
   * O suporte para CC (CEA 608/708) não está disponível, pois não é compatível com o CMAF.
   * O suporte para 4K ainda não está presente.
   * O suporte para tags ID3 não está disponível, pois não é compatível com o CMAF.
   * Fluxos de HEVC ao vivo não muxados não verificados.
   * Suporte a anúncios HEVC não verificado.
* Com a JIT ativada e a tolerância definida como 10 segundos, nenhuma chamada VAST será vista para o primeiro ad break intermediário se houver VMAP > anúncios de redirecionamento VAST.
* Para que a resolução do anúncio funcione corretamente, cada vez que a lista de reprodução é atualizada durante a reprodução de transmissão ao vivo, o reprodutor espera uma lista de reprodução compilada em 20 segundos. Se ele não receber uma lista de reprodução compilada dentro desse intervalo, um erro interno será lançado e o reprodutor será interrompido.

## Recursos úteis {#helpful-resources}

* [Guia do programador do TVSDK 3.4 para iOS](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [Referência da API do TVSDK iOS 3.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
