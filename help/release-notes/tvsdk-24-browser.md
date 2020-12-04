---
title: Notas de versão do navegador TVSDK 2.4
seo-title: Notas de versão do navegador TVSDK 2.4
description: As Notas de versão do Browser TVSDK 2.4 descrevem os recursos novos, compatíveis e não compatíveis e os problemas conhecidos no Browser TVSDK 2.4.
seo-description: As Notas de versão do Browser TVSDK 2.4 descrevem os recursos novos, compatíveis e não compatíveis e os problemas conhecidos no Browser TVSDK 2.4.
uuid: 3a1eb1a5-0e72-4658-beeb-bca8816570e7
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: d71886cb-f34b-47b2-9df7-168686478106
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '6834'
ht-degree: 0%

---


# Notas de versão do navegador TVSDK 2.4 {#browser-tvsdk-release-notes}

As Notas de versão do Browser TVSDK 2.4 descrevem os recursos novos, compatíveis e não compatíveis e os problemas conhecidos no Browser TVSDK 2.4.

## Introdução {#introduction}

O TVSDK do navegador é um kit de ferramentas que permite adicionar funcionalidade avançada de reprodução de vídeo, proteção de conteúdo e publicidade aos aplicativos de player de vídeo baseados em navegador.

O navegador TVSDK 2.4 fornece APIs JavaScript para criar aplicativos de vídeo baseados em navegador e inclui suporte para reprodução nos seguintes modos:

* Somente HTML5
* HTML5 com fallback de flash automático
* Flash sempre

Esta versão inclui as seguintes informações:

・ [Documentação da API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ [Guia de programação TVSDK do navegador](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ [TVSDK para 1.4 DHLS para o Guia de migração do Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ [Conversão do TVSDK 2.4.6 do navegador para a versão 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ Uma implementação de referência, que está incluída na compilação.

>[!NOTE]
>
>*Para obter uma lista completa das considerações de segurança desta versão, consulte Considerações de segurança.

## Novidades e recursos compatíveis {#what-s-new-and-supported-features}

Esta versão do TVSDK do navegador fornece novos recursos que você pode usar para aprimorar seus aplicativos de vídeo.

**Novo na atualização 2.4.12 (Build 204)**

A seguinte adição está disponível como parte da Atualização do Browser TVSDK 2.4.12 (Build 204):

* A implementação da API de volume do AdobePSDK.MediaPlayer foi alterada para permitir a reprodução automática no iOS quando a reprodução está silenciada.

・ Uma nova API, `auditudeSettings.ignoreVPAIDAds`, é adicionada para permitir que os anúncios VPAID recebidos do servidor Auditude sejam ignorados. A API não funciona para o fallback do Flash.

**Versão 2.4.11**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.11 do Browser TVSDK:

・ O failover de segmento do HLS Live é compatível com os modos de fallback de MSE e Flash.

・ O suporte para a API `AuditudeSettings.creativeRepackagingDomain` agora também está disponível para MSE. Anteriormente, era compatível somente com o modo de fallback de Flash.

・ A versão contém correções para problemas críticos do cliente. Consulte *Problemas corrigidos* uma lista.

**Versão 2.4.10**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.10 do Browser TVSDK:

・ O TVSDK fornece enableLogging() para ativar ou desativar o registro. Consulte a [documentação da API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)para obter detalhes sobre o uso.

・ O TVSDK não oferece mais suporte a Capítulos padrão ao usar o Adobe Analytics. Defina e gerencie capítulos usando seu aplicativo.

・ A versão contém correções para problemas críticos do cliente. Consulte *Problemas corrigidos *uma lista.

**Versão 2.4.9**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.9 do Browser TVSDK:

・ HLS VOD e fluxos ao vivo com descontinuidade de tempo, mas sem marcadores de descontinuidade, são suportados.

・ Os quadros ID3 v2.4.0 são compatíveis com a tag de vídeo Safari para fluxos VOD e ao vivo HLS.

・ A implementação do carregamento seguro do anúncio garante que as chamadas do servidor de anúncios sejam atualizadas para proteger o HTTP com base na configuração da API. Para obter detalhes, consulte AdobePSDK.AdvertisingMetadata e AdobePSDK.ForceHttpsAdConfiguration classes. Este recurso não é suportado no modo de fallback do Flash.

・ As informações de ID de anúncio e de extensão associadas às respostas do VAST 3.0 agora são disponibilizadas ao aplicativo pelo TVSDK e podem ser usadas para implementar a integração do Moat para medidas de anúncio. Para obter detalhes, consulte AdobePSDK.NetworkAdInfo API. Isso não é suportado no modo de fallback do Flash.

・ A classe AdobePSDK.ForceHttpsConfiguration não está mais disponível. É bem sucedido por

Classe AdobePSDK.ForceHttpsAdConfiguration.

・ Uma nova API, AdobePSDK.otimizeFlashCalls, agora está disponível para otimizar as chamadas para melhorar a experiência de reprodução de HLS no modo de fallback de Flash. Isso é desativado por padrão.

**Novo na atualização 2.4.8 (Build 6002)**

Esta atualização contém correções para problemas críticos do cliente. Consulte *Problemas corrigidos* para obter a lista.

**Versão 2.4.8**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.8 do TVSDK do navegador:

・ O SDK agora é compatível com o Chrome EME e as mudanças de práticas recomendadas disponíveis a partir do Chrome v58. Para obter mais detalhes, consulte [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ A Estrutura da interface agora suporta DRM de acesso HLS no Flash, somente publicidade e fluxo de trabalho de informações de definição de metas.

・ A API setDRMAuthenticateData é adicionada à Estrutura da interface do usuário. Para reproduzir fluxos protegidos com o DRM de acesso ao Adobe, chame esta API. Como alternativa, o atributo drmAuthenticateData pode ser especificado no player. Consulte [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)para obter detalhes.

**Versão 2.4.7**

Os seguintes recursos são novos na versão 2.4.7:

・ Adição do Configurador da interface de usuário na Estrutura da interface de usuário

Você pode configurar o player de uma das seguintes maneiras:

・ Uso de um objeto JSON

・ Usar APIs

Para ajudar a gerar o objeto JSON, o TVSDK do navegador fornece uma ferramenta **UI Configurator **.

Nesta ferramenta, você pode selecionar várias configurações, clicar em **Testar configuração **para verificar as configurações e clicar em **Download de configuração **para baixar as configurações. Depois de baixar o arquivo, você pode passar o conteúdo desse arquivo como objeto JSON para a API ptp.videoPlayer.

・ Adição da API MediaPlayerItemConfig à estrutura da interface do usuário

Vários recursos, incluindo anunciadataMetadata, anuncianteFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration, podem ser configurados por meio de MediaPlayerItemConfig. Para obter mais informações, consulte a documentação AdobePSDK.MediaPlayerItemConfig na [API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [documentação](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

Na UI Framework, a maneira de passar as configurações de rede pela configuração do player foi modificada.

**Versão 2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**Versão 2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* Suporte para workflows DRM e Analytics na UI Framework

As configurações de DRM e o rastreamento do Analytics podem ser habilitados por meio da UI Framework.

* Adição da API `AdobePSDK.embedSWFinFullScreenDiv`

Essa nova API fornece flexibilidade ao aplicativo do player para selecionar a div na qual ele pode incorporar o arquivo FlashFallback.swf.

* Substituída a API `getVersion`da classe `AdobePSDK.MediaPlayer` pela classe `AdobePSDK.Version` para obter informações relacionadas à versão do TVSDK. Para obter detalhes, consulte `AdobePSDK.Version` API [here](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versão 2.4.6**

Os seguintes recursos são novos na versão 2.4.6:

* **Suporte a navegação**

A opção Browserify permite que você use os módulos de estilo node.js no navegador. Você pode definir as dependências e Browserify agrupa tudo em um arquivo JavaScript.

* **Cobrança**

Com a ajuda do faturamento, o TVSDK do navegador pode coletar métricas de uso do player para faturar clientes do Primetime.

>[!NOTE]
>
>Os Eventos enum MediaPlayer.obsoletos e as constantes obsoletas em Enum PSDKErrorCode foram removidos na versão 2.4.6. Para obter mais informações, consulte [Conversão de TVSDK 2.4.5 do navegador para a versão 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versão 2.4.5**

Os seguintes recursos são novos na versão 2.4.5:

* **Reproduções e anúncios completos do Evento**

   Os fluxos HLS Full Evento Replay (FER) agora suportam a resolução do anúncio e os comportamentos do anúncio. Para ativar esse suporte, defina o modo de sinalização de anúncio como `MANIFEST_CUES` ao criar o objeto `MediaPlayerItemConfig`.

* **Suporte a ScalePolicy do MediaplayerView**

   Os desenvolvedores de aplicativos agora podem especificar uma scalePolicy diferente para a visualização usando a propriedade scalePolicy de MediaplayerView.

* **Suporte a conteúdo anamórfico**

   A reprodução de conteúdo anamórfico agora é compatível com o MSE e a reprodução do Flash.

* **Aplicação seletiva de`withCredentials`**

Quando `withCredentials` estiver definido como true, o cabeçalho `Access-Control-Allow-Origin` não poderá ser definido como um curinga. Dependendo da resposta do servidor, o TVSDK do navegador definirá seletivamente o atributo `withCredentials`. Para obter mais informações sobre esse suporte, consulte [Documentos da API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versão 2.4.4**

Os seguintes recursos eram novos na versão 2.4.4:

* **Aplicativo de amostra de cromecast**

Esta versão oferece suporte para um aplicativo remetente e receptor que demonstra a reprodução de fluxos VOD DASH e fluxos de viúvo DASH com inserção de anúncio no lado do cliente.

* **Suporte avançado a failover**

Esta versão contém suporte para casos de uso de failover avançado (failover de segmento e servidor) para fluxos VOD HLS.

**Versão 2.4.3**

Os seguintes recursos eram novos na versão 2.4.3:

* **Tags personalizadas para DASH VOD**

   Tags personalizadas embutidas (Eventos) podem ser assinadas e recebidas como objeto TimedMetadata.

* **Reprodução de fluxos sem extensões**

   Os fluxos HLS e DASH sem extensões agora são suportados. Para o arquivo manifest, o resourceType precisa ser especificado ao carregar o recurso. Para segmentos e arquivos VTT, o cabeçalho de resposta Content-Type é usado para determinar o tipo de conteúdo.

**Versão 2.4.2**

Os seguintes recursos eram novos na versão 2.4.2:

* **Paridade da API**

Para obter uma lista completa da paridade da API, consulte o [TVSDK para 1.4 DHLS para o Guia de migração do Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Suporte a AES de exemplo**

   Esta versão adiciona suporte para a reprodução de conteúdo criptografado AES de amostra em fallback de MSE e Flash. O requisito para hospedar conteúdo AES por origem segura no Google Chrome foi removido.

* **Suporte para container AAC**

   A reprodução de arquivos com a extensão .aac agora é compatível. Pode ser apenas streams de áudio ou áudio alternativo.

   >[!NOTE]
   >
   >AC3 e codecs AC3 aprimorados ainda não são suportados.

* **Reprodução de fluxo tokenized**

Os fluxos HLS que são entregues por meio de uma Rede de Delivery de Conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação, e esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookies. A reprodução desses fluxos agora é suportada.

**Versão 2.4.1**

Os seguintes recursos eram novos na versão 2.4.1:

* **Estrutura da interface do usuário**

Essa estrutura, projetada para acelerar o desenvolvimento da interface para aplicativos de player de vídeo baseados em JavaScript, consiste em APIs para incluir controles básicos como reproduzir/pausar e volume e para adicionar ou remover facilmente elementos como estados da barra de depuração e configurações de legenda fechada. Você pode especificar o comportamento associado aos controles, criar controles personalizados e mostrar a interface do usuário do player. Isso tudo acontece através da estrutura, sem a necessidade de manipular diretamente a estrutura do DOM.

* **Aprimoramentos de reprodução HLS para fluxos ao vivo**

Esta versão suporta descontinuidades causadas pela inserção de anúncios. Ele usa a tag EXT-PROGRAMA-DATE-TIME seguida pela tag EXT-MEDIA-SEQUENCE para sincronizar entre perfis adaptáveis de taxa de bits para uma reprodução suave.

* **Suporte a VPAID 2.0**

A definição da interface de serviço de anúncios do player de vídeo (VPAID), versão 2.0, fornece uma experiência de mídia avançada para os usuários e permite que os editores vejam anúncios de público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo. Esta versão é compatível com anúncios VPAID lineares do JavaScript para conteúdo VOD (Video-on-demand).

* **Tags HLS personalizadas**

Os fluxos de mídia podem conter metadados adicionais na forma de tags na lista de reprodução/arquivo manifest. O TVSDK do navegador permite que você especifique e assine tags adicionais e seja notificado quando essas tags forem exibidas no manifesto.

* **Marcadores de anúncio exibidos na linha do tempo do player**

Esta versão suporta a exibição de marcadores de anúncio na linha do tempo do player para conteúdo VOD e ao vivo. Você pode ver esse comportamento no player de referência.

**Suportado no 2.4**

Os seguintes recursos estavam disponíveis na versão 2.4:

* **Reprodução de áudio MP3**

   Esta versão oferece suporte à reprodução de áudio MP3 em navegadores com MSE (Media Source Extensions) e com a tag de vídeo Safari.

* **Reprodução de vídeo MP4**

   Os seguintes recursos são suportados:

   * Reprodução de fluxo único
   * Anúncios MP4 anteriores e posteriores à rolagem com comportamentos de anúncio e rastreamento
   * Anúncios HLS de pré e pós-rolagem com comportamentos de anúncio e rastreamento
   * Anúncios DASH de pré e pós-rolagem com comportamentos de anúncio e rastreamento

## Plataformas suportadas {#supported-platforms}

O TVSDK do navegador tem requisitos específicos para os níveis de plataformas e software necessários para execução. As seguintes plataformas e níveis de software são suportados:

### Configurações de desktop {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### Configurações da Web móvel {#mobile-web-configurations}

* Android 4.4

   * Navegador nativo
   * Chrome 33+

* Android 5.0

   * Navegador nativo
   * Chrome 33+

* Android 6.0

   * Chrome 33+

* Apple iOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast (segunda geração; apenas para reprodução DASH)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Tecnologia</strong> </p> </td> 
   <td><p><strong>Tag</strong><sup> 1 de vídeo TVSDK do navegador</sup></p> </td> 
   <td><p><strong>Navegador TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>Tecnologia padrão</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>Etiqueta de vídeo</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS e DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>Etiqueta de vídeo</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS e DASH</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS e DASH</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, PINCO</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de recursos {#feature-matrix}

Esta é uma lista dos recursos suportados e não suportados desta versão:

* *Recursos de áudio MP3 — Reprodução principal*
* *Recursos de vídeo MP4 — Reprodução principal*
* *Recursos de vídeo MP4 — Ad Insertion Core*

>[!NOTE]
>
>*Nas tabelas de matriz de recursos abaixo, um &quot;Y&quot; significa que o recurso é suportado na versão atual.*

### Recursos de áudio MP3 {#mp-audio-features}

**Tabela 1: Reprodução principal{#table-core-playback}**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD MP3 | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado | Y | Y |

1 A tag de vídeo TVSDK do navegador não suporta streaming e DRM. O suporte a codec e container não é o mesmo em todos os navegadores.

2 O Firefox assume como padrão o Flash Player para a versão 41 ou anterior.

### Recursos de áudio MP4 {#mp-audio-features-1}

**Quadro 2: Reprodução principal**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD MP4 | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado | Y | Y |

**Quadro 3: Ad Insertion Core**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD MP4 | Pré-rolo (MP4) | Não suportado | Y | Y |
| Ad Insertion | VOD MP4 | Pós-rolagem (MP4) | Não suportado | Y | Y |

Para obter mais informações sobre o suporte a recursos HLS ou DASH, consulte abaixo.

## Matriz de recursos HLS {#hls-feature-matrix}

Esta é a matriz de recursos para os recursos HLS na TVSDK do navegador.

* *Reprodução principal HLS*
* *Recursos de reprodução avançada HLS*
* *Recursos de proteção de conteúdo HLS*
* *Recursos de inserção de anúncio do HLS Core*
* *Recursos avançados de inserção de anúncios HLS*
* *Integrações HLS*

>[!NOTE]
>
>*Nas tabelas de matriz de recursos abaixo, um &quot;Y&quot; significa que o recurso é suportado na versão atual.*

### Recursos HLS {#hls-features}

Os seguintes recursos são suportados:

**Tabela 4: Reprodução principal HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reprodução geral (reprodução, pausa, busca)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Reprodução geral (reprodução, pausa e busca)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Taxa de bits adaptável</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Legendas 608/708</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Somente VOD</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover Manifest</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover avançado</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Notificações de QoS e player</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Suporte a QoS limitado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Suporte para cabeçalhos de cookies</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Definição de parâmetros de controle de buffer</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Definir adaptativo</p> <p>controles de taxa de bits</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tags personalizadas</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>Áudio de ligação tardia</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Redirecionamento 302</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 5: Recursos de reprodução avançada HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução em offset</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução somente de áudio</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução suave de truques</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Análise de ID3</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Suporte ao marcador de descontinuidade</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Fluxos Tokenized</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Cobrança</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 6: Recursos de proteção de conteúdo HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES de amostra</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Acesso ao Adobe</p> </td> 
   <td><p>Não suportado</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 7: Recursos de inserção de anúncio do HLS Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pré-rolo (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Meia rolagem (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Pós-rolagem (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Resolução e comportamentos do anúncio</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Política de publicidade padrão</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reembalagem criativa (MP4 para HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 8: Recursos avançados de inserção de anúncios HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Somente publicidade</p> </td> 
   <td><p>Não suportado</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Parâmetros de definição de metas</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Parâmetros personalizados</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Política de anúncio personalizada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Carregamento de anúncio ocioso</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Não suportado</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anúncios complementares, anúncios em banners, anúncios clicáveis</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 9: Integrações HLS{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrações</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integração Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de recursos DASH {#dash-feature-matrix}

Esta é a matriz de recursos dos recursos DASH na TVSDK do navegador.

・ *Recursos de reprodução principal DASH*

・ *Recursos avançados de reprodução do DASH*

・ *Recursos de proteção de conteúdo DASH*

・ *Recursos de inserção do anúncio principal do DASH*

・ *Recursos avançados de inserção de anúncios do DASH*

・ *Integrações DASH*

>[!NOTE]
>
>Nas tabelas de matriz de recursos abaixo, um Y significa que o recurso é suportado na versão atual.

### Recursos do DASH {#dash-features}

Os seguintes recursos são suportados:

**Quadro 10: Recursos de reprodução DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reprodução geral (reprodução, pausa, busca)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Reprodução geral (reprodução, pausa e busca)</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Taxa de bits adaptável</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Legendas 608/708</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Notificações de QoS e player</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Suporte para cabeçalhos de cookies</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Definição de parâmetros de controle de buffer</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Definir controles adaptáveis de taxa de bits</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tags personalizadas (EventStream)</p> </td> 
   <td><p>Somente VOD (em linha)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Áudio de ligação tardia</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Redirecionamento 302</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 11: Recursos de reprodução avançada DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução em offset</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução somente de áudio</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>peça</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução suave de truques</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Análise de ID3</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Suporte a vários períodos</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Fluxos Tokenized</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Cobrança</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 12: Recursos de proteção de conteúdo DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES de amostra</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Widevine no Chrome, Firefox 47 e posterior e Chromecast</p> <p>・ PlayReady no Internet Explorer no Windows 8.1 e Edge</p> <p>・ DRM Primetime para Windows Firefox (somente vídeo)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 13: Recursos de inserção de anúncio do DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pré-rolagem (MP4/DASH)</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Pós-rolagem (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Resolução e comportamento do anúncio</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Política de publicidade padrão</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reembalagem criativa (MP4 para DASH)</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 14: Recursos avançados de inserção de anúncios do DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Somente publicidade</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parâmetros de definição de metas</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parâmetros personalizados</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Política de anúncio personalizada</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Carregamento de anúncio ocioso</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anúncios complementares, anúncios em banner, anúncios clicáveis</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 15: Integrações DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo de conteúdo</strong></p> </td> 
   <td><p><strong>Recurso</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrações</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integração Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemas corrigidos {#issues-fixed}

**Problemas corrigidos na atualização 2.4.12 (Build 204)**

Os seguintes problemas foram corrigidos na Atualização do Browser TVSDK versão 2.4.12 (Build 204):

・ **21647**- O TVSDK deve permitir a reprodução automática de vídeo em dispositivos iOS quando o áudio estiver sem áudio.

・ **21465**- O Acesso Negado ao Sistema de Chave de Erro é recebido ao reproduzir um fluxo DASH protegido por DRM depois que um fluxo DASH Live é reproduzido.

・ **21442**- Habilite a reprodução automática de conteúdo na Web do iOS, depois que o anúncio de pré-lançamento for reproduzido com um gesto de usuário.

・ **21240**- API fornecida para filtrar anúncios VPAID analisados do Auditude/VMAP.

**Problemas corrigidos na versão 2.4.11**

Os seguintes problemas foram corrigidos no navegador TVSDK versão 2.4.11:

**Recursos principais de reprodução:**

・ **19192**: O TVSDK agora implementa TextFormat:bottomInset e TextFormat:safeArea. Devido a esses aprimoramentos, as legendas ocultas podem ser posicionadas novamente se a barra de controle for exibida na tela.

・ **21009**: As legendas ocultas persistem na tela em caso de busca durante a descontinuidade até que novas legendas sejam exibidas.

・ **21141**: A busca é rejeitada devido a uma condição de corrida durante a anexação do segmento.

・ **21142**: Disponibilizando intervalos de reprodução pesquisáveis quando o player estiver em estado INICIALIZADO. Devido a essas alterações, a sessão do start na posição agora é suportada.

・ **21363**: As legendas 608/708 estão saindo de sincronia após a inserção do anúncio para fluxos DASH.

**Recursos de inserção de anúncios:**

・ **21179**: Problemas relacionados ao intermediário (pausas longas, quadros pretos) com conteúdo VOD agora são resolvidos definindo corretamente a propriedade ad.PrimaryAsset.adParameters.

・ **21257**: O arquivo MP4 com a maior taxa de bits é selecionado para transcodificação se MP4 não for um tipo MIME válido e o recurso de reempacotamento criativo estiver ativado.

・ **21361**: O TVSDK agora passa a ID criativa e do sistema de anúncios da resposta VAST como parâmetros de query na solicitação de pacote criativo para suportar regras adicionais de normalização.

**Problemas corrigidos na versão 2.4.10**

Os seguintes problemas foram corrigidos no navegador TVSDK versão 2.4.10:

**Recursos principais de reprodução:**

・ **21060**: Erro de codec inválido lançado com fluxos HLS que contêm descontinuidade e as caixas BMFF ISO são executadas até o fim do fluxo.

・ **21045**: A reprodução automática não funciona no iOS depois que a primeira reprodução de vídeo em uma lista de reprodução é concluída.

・ **20975**: A taxa de quadros é retornada como NaN pelo provedor QoS no navegador Chrome.

・ **20823**: Erro de codec não suportado lançado ao encontrar segmentos sem dados.

・ **20769**: O SDK agora é start com a taxa de bits atual em busca em vez de alternar imediatamente com base na política ABR.

・ **20031**: Quando no modo retrato no IE11 (Windows 8.1), a tela de vídeo fica pequena. Recurso de proteção de conteúdo:

・ **19316**: Ignore os segmentos que falham na descriptografia no caso de fluxos HLS AES-128.

**Problemas corrigidos na versão 2.4.9**

Os seguintes problemas foram corrigidos no navegador TVSDK versão 2.4.9:

**Recursos principais de reprodução:**

・ **13407**: Os fluxos DASH podem parar se o Firefox parar de enviar eventos &quot;ontime update&quot; durante a reprodução.

・ **16380**: Durante a reprodução de conteúdo de vídeo em áudio muxed de segmentos com tempos de start não correspondentes via MSE, o erro de sincronização de áudio entre representações é acumulado em switches ABR, resultando em erro (problema de crômio nº 663686).

・ **17985**: Ao reproduzir um fluxo ISO-BMFF específico no navegador Firefox, a reprodução fica travada (problema do Firefox nº 1342913). Isso foi corrigido desde o Firefox v53.

・ **19141**: ReferenceError não capturado (em promessa): largura não é definida.

・ **18997, 19299**: Problema de oscilação de vídeo no limite do segmento. Isso ocorria porque o SDK não calculava corretamente o deslocamento de tempo de Composição da última amostra.

・ **19780**: A reprodução não é start para conteúdo HLS e Anúncio HLS no Firefox v53 (edição n.º 354653 do Firefox).

・ **20046**: A Data e hora do programa é recebida como chave em vez de valor quando recebida como objeto de metadados cronometrados.

・ **20047**: useDefaultResizeHandler lança um erro com o fallback do Flash.

・ **20179**: Falha de Flash que não funciona com o Flash Player v25.0.0.171.

・ **20293**: O Firefox interrompe os dados de buffering para determinados fluxos HLS que levam à paralisação.

・ **20626**: O player lança um erro de decodificação de mídia no Chrome devido ao tratamento incorreto de amostras de vídeo com duração zero.

・ **20078**: A reprodução é interrompida no erro de navegador &#39;QuotaExceeded&#39;.

・ **18639**: No HLS Live stream 608 CC, o texto às vezes aparece como ortografia incorreta.

・ **20028**: O parâmetro de tamanho ClosedCaptions não altera o tamanho da fonte.

・ **20613**: Caixas de legendas ocultas se sobrepõem umas às outras tornando-as ilegíveis.

**Recursos do Ad Insertion principal (CSAI):**

・ **20043**: Impressão de anúncio ausente e chamadas de rastreamento de anúncio com vários anúncios e redirecionamentos de terceiros.

・ **2004**: Ao usar o reempacotamento criativo, todos os anúncios no intervalo do anúncio precisam ser reempacotados com êxito, caso contrário, o intervalo do anúncio será totalmente descartado.

・ **20097**: A reprodução do anúncio é ignorada e o conteúdo principal é retomado imediatamente em vez de aguardar 20 segundos se o manifesto do anúncio não estiver disponível.

**Problemas corrigidos na atualização da versão 2.4.8 (Build 6002)**

Os seguintes problemas foram corrigidos na Atualização do Browser TVSDK versão 2.4.8 (Build 6002):

・ **14126:** A reprodução pode parar no Firefox (problema nº 1316024) devido a uma lacuna interna no buffer de origem MSE. Tente procurar para retomar a reprodução

・ **19608:** Correção para honrar o valor do deslocamento de tempo da resposta Auditude VMAP.

・ **19635:** Corrige o Video Stall no Internet Explorer 11 no Windows 10.

・ **19761:** Correções para problemas de ABR com HLS.

・ **19780:** Corrige a reprodução do anúncio com conteúdo HLS que foi quebrado no Mozilla Firefox v53.

・ **1987 e 19744:** Os problemas corrigem a inconsistência na seleção da taxa de bits após uma operação de busca. Agora, a seleção da taxa de bits em busca é o valor mais baixo da taxa de bits atual e da taxa de bits no start.

・ **19881:** A sobreposição de reprodução travada e de buffering é exibida por um tempo infinito após a busca ser executada por 3 a 4 vezes.

・ **19884:** Confirmar a conformidade com os requisitos do Chrome 59 Beta Verified Media Path (VMP). O bTVSDK conseguiu reproduzir o conteúdo do DRM do Widevine com o Chrome 59 Beta.

・ **19916:** A reprodução de DRM na UI-Framework foi interrompida. Agora, ele chama acquisitionLicense mesmo se não houver política nos metadados.

**Problemas corrigidos na versão 2.4.8**

Os seguintes problemas foram corrigidos na versão 2.4.8 do Browser TVSDK:

・ **10075**: Ao buscar antes da linha do tempo, o evento de reprodução concluída não foi recebido no Firefox e no Chrome e o evento de busca não foi recebido no Firefox.

・ **15775**: Reproduzir evento concluído não recebido no Windows 8.1 Internet Explorer.

・ **17306**: Para fluxos SSAI, a reprodução é suportada. Não há suporte para o rastreamento de anúncios agrupados.

・ **19142**: Às vezes, rebobinar faz com que o player de vídeo permaneça no estado de buffering para sempre.

・ **19218**: Os marcadores de anúncios não estão disponíveis por meio da estrutura da interface do usuário.

・ **19219**: A reprodução de anúncios só não funciona pela estrutura da interface do usuário.

・ **1922**: A chave AES-128 é solicitada uma vez para uma lista de reprodução e as solicitações subsequentes são atendidas do cache. Anteriormente, era solicitado para cada segmento.

・ **19597**: &quot;TypeError não detectado: &quot;Não é possível ler a propriedade &quot;log&quot; de indefinido&quot; foi vista com compilações do Chrome canary.

・ **19605**: adRequestDomain não estava disponível quando estava no modo Fallback de Flash.

・ **19608**: Anúncios VMAP não estavam sendo inseridos para fluxos do HLS Live. O SDK agora considera os marcadores de sinalização e não depende dos valores de deslocamento de tempo nas respostas do VMAP.

・ **19637**: A reprodução somente de anúncios leva a um erro de script no fim do anúncio.

・ **19732**: As solicitações da lista de reprodução do CRS falhavam com o erro 404. As solicitações 1401 e 1403 do TVSDK do navegador agora são atualizadas para cuidar disso.

・ **19762**: acquisitionLicense costumava ser chamado antes de setAuthenticationToken por causa do qual uma licença válida era devolvida independentemente da validade do token. Isso foi corrigido agora e o acquisitionLicense é chamado somente após a resposta setAuthenticationToken.

**Problemas corrigidos na versão 2.4.7**

Os seguintes problemas foram corrigidos na versão 2.4.7:

・ **8397**: Os fluxos ao vivo do HLS gerados pelo Adobe Media Server podem não ser reproduzidos se os segmentos não forem start com um quadro chave.

・ **13606**: Vários problemas relacionados ao Seek corrigidos para fluxo HLS no navegador Chrome.

・ **14807**: No navegador Chrome, se a busca ou pausa for acionada imediatamente após play(), a reprodução pode parar com o erro DOMException: A solicitação play() foi interrompida por uma chamada...(Problema com crômio nº 593273).

・ **19085**: Os parâmetros MediaPlayer, como volume, abrControlParameters e ccStyle, não estão definidos como Padrões na Redefinição do Player.

**Problemas corrigidos na versão 2.4.6**

O seguinte problema foi corrigido na versão 2.4.6:

・ **18093**: TimedMetadata para a tag próxima à tag assinada é retornada quando você usa a versão 24 do Flash Player no modo de Fallback do Flash.

**Problemas corrigidos na versão 2.4.4**

Os seguintes problemas foram corrigidos na versão 2.4.4:

・ **8711**: Com o MSE, as legendas 608/708 são justificadas por padrão.

・ **13934**: As configurações de ABR para anúncios não se aplicam ao reproduzir com fluxos ao vivo do HLS.

・ **14079**: A longevidade para fluxos ao vivo do HLS com uma janela do DVR baixa pode falhar, pois a reprodução pode estar atrasada devido a problemas de latência da rede. Clique no ponto ativo para retomar a reprodução.

・ **15037**: As amostras enviadas com a estrutura da interface do player não funcionam no Microsoft Internet Explorer 10 no Windows 7.

・ **15913**: Para fluxos VOD HLS, no Chrome, o fluxo não será reproduzido se a resposta do manifesto não for 304 modificada. Isso foi corrigido desde o Chrome v55 (Chromo issue 633696).

・ **16103**: No Android Chrome, em condições de largura de banda baixa, a reprodução pode travar com o TypeError não detectado: Não é possível ler a propriedade &#39;programDateTime&#39; de um erro indefinido.

・ **16265**: Para fluxos VOD e VOD ao vivo HLS, a busca por descontinuidades não funciona.

・ **16709**: A retomada do fluxo ao vivo HLS com PDT e marcador de descontinuidade pode levar o player a ficar preso no buffer.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

As limitações e os problemas conhecidos no TVSDK do navegador são mencionados abaixo.

**Quadro 16: Principais recursos de reprodução**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (apenas reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Reprodução geral (Reproduzir, Pausar, Buscar)</td> 
   <td><p>・ Não há suporte para formatos de mídia diferentes de HLS.</p> <p>8799: O fallback do Flash não cuida de conteúdo misto e, portanto, é necessário garantir que Conteúdo, Publicidade e outros URLs não levem a conteúdo misto (conteúdo seguro e inseguro juntos).</p> <p>19271: A reprodução de várias visualizações por meio da estrutura da interface não é suportada no modo de fallback do Flash.</p> <p>・ O fallback do Flash não funciona no Microsoft Internet Explorer 8 e 9 no Windows 7, pois essas versões não são suportadas pelo SDK.</p> <p>・ 20262: Flash fallback adiciona parâmetros personalizados à lista de informações de direcionamento. Além disso, a ordem de prioridade dos parâmetros personalizados é diferente no caso de Flash e MSE.</p> <p>・ 20653:O fallback do Flash TVSDK do navegador não funciona no Win10 com a Atualização do criador.</p> <p>・ O Flash Fallback funciona com o Flash Player versão 23 e posterior.</p> <p>・ 20087 - Chrome 59 Beta com</p> <p>Flash 25.0.0.171</p> <p>Beta(padrão), a reprodução HLS não está funcionando no modo de fallback de Flash. Está funcionando bem no Canário.</p> </td> 
   <td><p>12563: Os Dash Streams com codec de áudio mp4a.40.02 não são reproduzidos no Firefox devido à sequência de codec de áudio não compatível no MPD. Codec de áudio mp4a.40.2 é suportado.</p> <p>15029: Ao alternar entre vídeos em multiView na UI-Framework, o botão reproduzir/pausar não é atualizado adequadamente.</p> <p>・ 16034:No Windows 8.1 IE, chamar reset() leva a um erro de tipo MIME desconhecido. Recarregue a mídia para retomar a reprodução.</p> <p>・ 18235: Alguns problemas de busca são observados com fluxos de vídeo DASH com anúncios.</p> <p>18727: A API de erro não é compatível com MSE</p> <p>18750: Eventos de Alteração de status podem estar fora de ordem em alguns casos para a estrutura do SDK e da interface do usuário e na Estrutura da interface do usuário, eventos IDLE e Initializing StatusChange podem estar ausentes para os ouvintes de evento adicionados depois que o recurso é carregado.</p> <p>・ 18889: Se o MediaPlayer estiver no estado ERROR, o objeto de visualização não será retornado.</p> <p>・ 19039: Se o AdobePSDK. MediaPlayer. O searchToLocal() é usado com um valor maior que EOF e, em seguida, start de reprodução do início no caso de MSE.</p> <p>・ 19049: Nenhum estado de erro relatado para Flash Player no Chrome, IE e Firefox quando o vídeo é bloqueado durante a reprodução.</p> <p>・ 17205: A reprodução de vídeo é interrompida durante a reprodução de fluxo contínuo sem mudo por algumas horas enquanto o áudio continua sendo reproduzido (Problema de crômio nº 664033).</p> <p>・ 12308: Fluxos DASH com o valor distribution_time_offset especificado podem ter timeStampOffset aplicado a ele no navegador Chrome, resultando em tempo de decodificação negativo e, portanto, erro MEDIA_ERR_ SRC_NOT_ SUPPORTED (problema Chromo #398141).</p> <p>14126: A reprodução pode travar no Firefox (problema nº 1316024) devido a uma lacuna interna no buffer de origem MSE. Tente procurar para retomar a reprodução.</p> <p>19115: O MS Edge e o IE 11 (Win 8.1 e 10) não definem a Origem como nula no redirecionamento do CORS e ainda falham porque o cabeçalho não é nulo, resultando em erro de reprodução.</p> <p>・ 19861:Problema com comportamento de anexação no buffer de origem para mídia já reproduzida. O Chrome rejeita o fragmento anexado, incluindo moov, causando um erro de decodificação subsequente. (Problema com crômio nº 735335)</p> <p>19921: A reprodução é paralisada para determinados conteúdos HLS, mesmo que seu buffer tenha sido feito com êxito (edição Chromine nº 713540)</p> <p>・ 2044:A busca pelo fim do intervalo armazenado em buffer no IE e no Edge pode fazer com que a reprodução seja interrompida.</p> <p>・ 20511: Às vezes, a busca de rejeição pode ser observada para fluxos HLS com ou sem anúncios.</p> <p>・ 20743: No Windows 10 Chrome, o fluxo do HLS Live é reproduzido por alguns segundos antes da reprodução da pré-rolagem MP4.</p> <p>・ 21043: A dimensão de vídeo pode não estar correta na carga inicial devido à falta de metadados.</p> <p>21115: O gesto do usuário do Android é necessário para a reprodução do start se o anúncio precedente estiver disponível para vídeos em uma lista de reprodução.</p> <p>・ O HLS Live não oferece suporte à rolagem do carimbo de data e hora.</p> <p>・ O áudio AAC-SSR não é suportado.</p> <p>Os codecs de áudio AC3 e AC3 aprimorados não são suportados.</p> <p>・ Para fluxos com descontinuidade de carimbo de data e hora, mas sem marcadores de descontinuidade</p> <p>・ A reprodução pode apresentar falhas e uma busca incorreta devido a saltos.</p> <p>・ A duração e a duração da reprodução do conteúdo podem não corresponder.</p> <p>・ As descontinuidades entre representações e representações devem corresponder a outros problemas de sincronização e paralisação.</p> <p>・ As legendas e a WebVTT podem não aparecer perto do fim do fluxo.</p> <p>・ Alterações de codec de áudio não são suportadas em saltos de carimbo de data e hora.</p> <p>・ A inserção de anúncios não é suportada.</p> <p>・ O modo de truque avançado rápido pode levar a um loop de reprodução no Win 8.1 IE 11 (edição MS nº 12446268).</p> <p>TRAÇO:</p> <p>・ Para fluxos ao vivo - o perfil ao vivo com tipo dinâmico é suportado.</p> <p>・ Para fluxos VoD - o perfil ao vivo com tipo estático é suportado.</p> <p>Para fluxos VoD - o perfil sob demanda não é certificado para workflows de anúncios.</p> </td> 
   <td><p>・ Os fluxos DASH Live e DASH Video on Demand não são suportados.</p> <p>A reprodução de vídeo PIP(Picture in Picture) não é suportada no modo de tela cheia no iOS.</p> <p>Na extensão Safari (Etiqueta de vídeo), menos manifesto sem ter um cabeçalho de tipo de conteúdo correto não funciona.</p> </td> 
   <td><p>・ a applicationID no aplicativo remetente precisa ser a mesma gerada ao registrar o URL do Destinatário como um aplicativo Destinatário personalizado.</p> <p>O player de referência é certificado para workflows DASH. A estrutura da interface do usuário não está certificada.</p> <p>Para obter a lista dos codecs de mídia suportados, consulte <a href="https://developers.google.com/cast/docs/media"><em>here</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Reprodução geral (Reproduzir, Pausar, Buscar)</td> 
   <td> </td> 
   <td>18098: Determinados problemas de busca são observados com o fluxo HLS LBA FER.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Taxa de bits adaptável</td> 
   <td><p>・ 20079: Regravação de buffer na busca dentro do intervalo armazenado em buffer.</p> <p>20080: O comportamento ABR do Flash é consistente com o MSE.</p> </td> 
   <td><p>・ A variante de fallback somente de áudio em um fluxo ABR é ignorada devido a limitações relacionadas ao buffer.</p> <p>12289: Os parâmetros de controle ABR não se aplicam ao áudio no caso de fluxos HLS/DASH sem mudo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Legendas 608/708</td> 
   <td> </td> 
   <td><p>7810: No Android 4.4.4, o Chrome não parece ter suporte para famílias básicas de fontes CSS usadas pelo player e, portanto, a função de alteração de estilo de fonte não está funcionando.</p> <p>・ Os canais CC não podem ser alterados no caso de 608 legendas.</p> <p>・ Recursos avançados de estilização não são suportados para 608 legendas.</p> <p>Legendas incorporadas (608/708), sinalizadas por meio da tag de acessibilidade são suportadas.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>5206: As marcas de região no arquivo WebVTT são ignoradas pelo player ao exibir as legendas.</p> <p>DASH: Arquivos VTT fragmentados/segmentados não são suportados.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover manifesto</td> 
   <td>21056: Com o fallback do Flash, o Failover não ocorre para o fluxo ao vivo se o fluxo principal retornar um erro 404 durante a reprodução.</td> 
   <td>O failover de manifesto é aplicável somente para conteúdo e não para anúncios.</td> 
   <td>O failover da lista de reprodução ausente funciona somente no Safari para o código de erro HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover avançado</td> 
   <td> </td> 
   <td><p>・ O failover de segmento não suporta ignorar segmentos indisponíveis e continuar a reprodução.</p> <p>20533: Segmentos ausentes em uma lista de reprodução devem ser tratados como Descontinuidade e a reprodução deve retomar do próximo segmento disponível.</p> <p>21267: A alternância de fluxos devido a failover pode levar ao download de segmentos mais antigos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Notificações de QoS e Player</td> 
   <td>21129: A taxa de quadros não está disponível no caso de Fallback de Flash.</td> 
   <td><p>11170:</p> <p>Timed_Evento não está disponível para TVSDK do navegador com MSE, ao contrário do TVSDK do navegador com Fallback de Flash.</p> <p>21129: A taxa de quadros não é calculada para fluxos ao vivo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Suporte para cabeçalhos de cookies</td> 
   <td> </td> 
   <td> </td> 
   <td><p>o sinalizador withCredentials e os cabeçalhos de cookie não são suportados no Safari.</p> <p>21051: Para permitir cookies no Safari, ative a configuração "Cookies e dados do site" em Preferências &gt; Privacidade.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Tags personalizadas</td> 
   <td>14763: Tags personalizadas que não iniciem com # não devem ser suportadas. No momento, o objeto TimedMetadata é criado e relatado para essas tags durante o fallback do Flash.</td> 
   <td>Os fluxos com tags personalizadas em banda não são certificados.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Áudio de ligação tardia</td> 
   <td> </td> 
   <td><p>・ A inserção de anúncios não é suportada com fluxos HLS Live LBA.</p> <p>17273: Os fluxos de HLS VOD LBA alternam para a execução padrão no caso de failover e não podem ser alternados de volta para a última seleção.</p> <p>・ 20251: O fluxo de LBA ao vivo do HLS pode parar na busca.</p> <p>・ 20497: O player permanece no estado de buffering se os fluxos sem mudo do LBA HLS tiverem quadros de áudio ou vídeo ausentes próximos ao fim do fluxo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Redirecionamento 302</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>a otimização de redirecionamento não é suportada em navegadores Windows Edge e IE, pois eles não suportam a propriedade responseURL no objeto XMLHttpRequest.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 17: Recursos avançados de reprodução**

<table> 
 <tbody> 
  <tr> 
   <td>Tipo de conteúdo</td> 
   <td>Recurso</td> 
   <td>Flash</td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (apenas reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reprodução em offset</td> 
   <td><p>O início da reprodução em um valor de deslocamento específico não é compatível com o conteúdo MP4.</p> </td> 
   <td>20492: Anúncios intermediários que precedem o deslocamento são reproduzidos antes que o conteúdo seja retomado do valor de deslocamento.</td> 
   <td>A reprodução com recurso de deslocamento não é compatível com o iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>A reprodução de opções suave não funciona para fluxos sem execuções de iFrame.</td> 
   <td><p>・ As adaptações do Trick Play não são compatíveis com o Firefox e o Internet Explorer e, portanto, o modo de truque reverso não está disponível nesses navegadores.</p> <p>・ O recurso Trickplay não está disponível ao reproduzir conteúdo junto com anúncios.</p> <p>・ 10435: Durante a reprodução do DASH, o vídeo congela na reprodução de truques avançados no Internet Explorer (Win 8.1)</p> <p>intermitentemente. Isso ocorre porque estamos usando a propriedade playbackRate dos elementos de vídeo sem a adaptação da reprodução de truques.</p> <p>14182: Às vezes, durante o rebobinamento no navegador Chrome, o evento de busca pode não ser recebido e, portanto, o modo de truque não funcionará.</p> <p>14942: As taxas de reprodução podem ser definidas no Chrome para Android mesmo no caso de fluxos de reprodução sem truques, mas a configuração não será aplicada e a reprodução continuará em uma taxa normal.</p> <p>・ 17308: A busca não funciona no modo Trickplay.</p> <p>・ 17309: No navegador Chrome, o modo de truque reverso não pode ser mantido por mais de 2 segundos.</p> <p>19272: A reprodução de truques pode não se recuperar do buffering no navegador Windows 10 Edge no caso de fluxos DASH.</p> </td> 
   <td>O modo de truque de retrocesso não é suportado.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Análise do ID3</td> 
   <td>20346: O byte de codificação de texto de quadros ID3 também deve ser retornado pelo SDK.</td> 
   <td><p>As tags ID3 disponíveis nos fluxos de transporte de dados de áudio (ADTS) são ignoradas pelo SDK.</p> <p>12378: Os metadados cronometrados ID3 são analisados em momentos diferentes no Flash e no navegador com suporte a MSE e, portanto, o comportamento de exibição na linha do tempo do player de referência também é diferente.</p> <p>19247: A análise de ID3 não é suportada na estrutura da interface do usuário.</p> </td> 
   <td><p>・ 20323: A tag PRIV ID3 usada para sinalizar o carimbo de data e hora da primeira amostra de segmento aac não é analisada pelo Safari (edição Safari #32422733)</p> <p>・ 20350: Em certos dispositivos (incluindo MAC OS X 10.1, iPad10), o Safari não fornece evento de mudança de sinalização quando em modo de truque e, portanto, quadros ID3 não são recebidos. (Problema no Safari #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Suporte ao marcador de descontinuidade</td> 
   <td> </td> 
   <td><p>・ A inserção de anúncio do lado do cliente não é suportada com fluxos HLS contendo descontinuidade.</p> <p>・ A alteração do codec de áudio não é permitida em descontinuidades no fluxo HLS.</p> <p>・ O switch de faixa de áudio não é compatível com fluxo HLS com marcadores de descontinuidade</p> </td> 
   <td>O número de sequência de descontinuidade é um requisito para fluxos HLS com descontinuidade para reprodução no Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 18: Recursos de proteção de conteúdo**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (apenas reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>O intervalo de bytes não é suportado com conteúdo criptografado AES-128.</td> 
   <td>12324: Os fluxos criptografados HLS AES-128 falharão na reprodução no Safari se a tag IV não for especificada.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>12660: O player HTML5 lança um erro interno do servidor para conteúdo de hífen criptografado PlayReady expirado.</p> <p>16720: O conteúdo criptografado por DRM DASH não funcionará se o atributo do start na tag period estiver ausente.</p> <p>・ 18589: A reprodução não é suportada para fluxos de vários períodos DRM VoD protegidos por DRM com Xlink.</p> <p>・ 18653: Reprodução de Conteúdo de Vários Períodos do Widevine com Múltiplas Chaves, interrompe no primeiro período e não pode alternar para o próximo.</p> <p>・ 18656: O Playready MultiPeriod Stream, criptografado com chaves diferentes, não é reproduzido.</p> <p>O Playready 2.0 para Dash não está certificado.</p> <p> </p> <p> </p> </td> 
   <td>12602: Metadados DRM do HLS Fairplay são atualizados repetidamente pelo player HTML5 no Safari</td> 
   <td><p>O conteúdo DRM de widevine DASH empacotado por meio do Bento4 pode ser reproduzido. O conteúdo empacotado por meio da Offline Packager e do Shaka Packager não é reproduzido. DASH PlayReady DRM não é suportado.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 19: Recursos do Ad Insertion Core (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (apenas reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Pré/Médio/Post</td> 
   <td> </td> 
   <td><p>・ Anúncios anteriores com conteúdo em tempo real HLS são reproduzidos no modo de reprodução dupla.</p> <p>・ Anúncios DASH com conteúdo HLS e anúncios HLS com conteúdo DASH não são suportados.</p> <p>19002: Em HTML5 Player com MSE adBreak. O insertType não retorna o valor correto para descrever o tipo de inserção correto, isto é, o cliente foi inserido e ou o servidor foi inserido.</p> <p>7794: Em dispositivos móveis (iOS, Android com Chrome 33 ou inferior ou Navegador nativo) onde a barra de controle padrão está visível no modo de tela cheia, a barra de busca e os botões de avanço rápido estão disponíveis quando o Ads Play.</p> <p>11048: Alternar de anúncio para conteúdo do HLS Live não é suave no caso de Extensões de origem de mídia.</p> <p>・ 16083: No Android 4.4 Chrome v52, às vezes os anúncios HLS com conteúdo HLS podem levar a erro de decodificação de pipeline após a reprodução parada.</p> <p>・ 16097: Os erros encontrados durante a pausa do anúncio não são tratados, podem fazer com que o fluxo principal pare a reprodução.</p> <p>・ 18095: Anúncios MP4 não são suportados com conteúdo ativo HLS.</p> <p>19120: Várias buscas em anúncios HLS com conteúdo HLS podem fazer com que o fluxo pare a reprodução.</p> <p>19131: A sobreposição de buffer pode aparecer ao alternar da pausa de anúncio precedente para o conteúdo.</p> <p>・ 20296: No caso de streams ao vivo do HLS, a busca de volta na janela do DVR seguida pela busca em rolagens médias resolvidas pode levar à parada da reprodução.</p> <p>・ 20298:HLS Live streams com rolls mid roll (rolagem intermediária) encerra o momento em que o primeiro mid roll (mid roll-roll) e se move para fora da janela do DVR.</p> <p>・ 20317: Os fluxos ao vivo do HLS podem travar ao alternar para o próximo anúncio ou de anúncio para conteúdo, caso o intervalo do anúncio contenha mais de um anúncio.</p> 
    <ul> 
     <li>Os anúncios na janela DVR de fluxos ao vivo do HLS não são resolvidos.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>O SDK não honra o atributo de sequência dentro da resposta VMAP para VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>2079: O SDK não honra o atributo de sequência dentro da resposta VMAP para VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: O atributo de repetição VMAP não é suportado.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Reempacotamento da criação</td> 
   <td> </td> 
   <td>21464: A resposta do anúncio é totalmente descartada se a reembalagem criativa falhar em um dos anúncios no intervalo do anúncio.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 20: Recursos avançados do Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (apenas reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Somente publicidade</td> 
   <td> </td> 
   <td>20056: A propriedade da tecnologia do player não é relevante, pois se baseia no conteúdo principal que está vazio no caso de reprodução Somente anúncio</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Política de anúncio personalizada</td> 
   <td> </td> 
   <td><p>・ Comportamentos de anúncios não são suportados com anúncios MP4 e conteúdo MP4.</p> <p>・ 13973: Comportamentos de anúncio personalizados - a política de SKIP não gera evento completo quando usada com MSE.</p> <p>・ 14939: As políticas personalizadas de comportamento de anúncio ignoram e ignoram a quebra de anúncio não estão funcionando para o conteúdo DASH.</p> <p>17131: O primeiro quadro do anúncio está visível e o conteúdo é retomado no caso de política de quebra de anúncio SKIP.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Anúncios complementares/banners/ anúncios clicáveis</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Anúncios de banner não ficam visíveis ao usar o player de referência.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ Comportamentos de anúncios não são suportados para anúncios VPAID.</p> <p>・ 15032: Anúncios VPAID em combinação com anúncios MP4 ou HLS em uma pausa de anúncio não são suportados.</p> <p>19001: No Android e no iOS, quando o anúncio VPAID é reproduzido com MP4, pois as faixas de áudio do duplo de conteúdo principal são audíveis, um dos conteúdos principais e um dos anúncios.</p> <p>・ 20762: Anúncios VPAID não são compatíveis com Picture in Picture (PIP).</p> <p>21172: Reproduzir evento concluído não é recebido para conteúdo VOD HLS com anúncios VPAID.</p> <p>21173: onAdBreakCompleteEvent não é recebido para conteúdo VOD de HLS e anúncios VPAID de post roll.</p> </td> 
   <td>O player alterna entre o modo normal e o modo de tela cheia ao alternar entre o conteúdo VPAID e Principal.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 21: Integrações**

| **Tipo de conteúdo** | **Recurso** | **Flash** | **HTML5 no Firefox, IE, Chrome, Android Chrome** | **HTML5 no Safari, iOS Safari** | **Chromecast (apenas reprodução DASH)** |
|---|---|---|---|---|---|
| VOD + Live | Integração Adobe Analytics VHL |  | 19004: O rastreamento do Video Analytics não está disponível por meio da ferramenta de configuração de interface do usuário. |  |  |

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte da Adobe Primetime](https://helpx.adobe.com/support/primetime.html).