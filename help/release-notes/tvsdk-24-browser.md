---
title: Notas de versão do Browser TVSDK 2.4
description: As Notas de versão do Browser TVSDK 2.4 descrevem os recursos novos, compatíveis e não compatíveis e os problemas conhecidos no Browser TVSDK 2.4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Notas de versão do Browser TVSDK 2.4 {#browser-tvsdk-release-notes}

As Notas de versão do Browser TVSDK 2.4 descrevem os recursos novos, compatíveis e não compatíveis e os problemas conhecidos no Browser TVSDK 2.4.

## Introdução {#introduction}

O TVSDK do navegador é um kit de ferramentas que permite adicionar funcionalidades avançadas de reprodução de vídeo, proteção de conteúdo e publicidade aos aplicativos do player de vídeo baseados em navegador.

O Browser TVSDK 2.4 fornece APIs JavaScript para criar aplicativos de vídeo baseados em navegador e inclui suporte a reprodução nos seguintes modos:

* Somente HTML5
* HTML5 com fallback de flash automático
* Flash always

Esta versão inclui as seguintes informações:

・ ・ [Documentação da API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ ・ [Guia de programação TVSDK do navegador](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ ・ [TVSDK para DHLS 1.4 para Guia de migração do Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ ・ [Conversão do Browser TVSDK 2.4.6 para a versão 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ Uma implementação de referência, que está incluída na build.

>[!NOTE]
>
>*Para obter uma lista completa das considerações de segurança desta versão, consulte Considerações de segurança.

## Novidades e recursos compatíveis {#what-s-new-and-supported-features}

Esta versão do Browser TVSDK fornece novos recursos que podem ser usados para aprimorar seus aplicativos de vídeo.

**Novo na atualização 2.4.12 (Build 204)**

A seguinte adição está disponível como parte da Atualização do Browser TVSDK 2.4.12 (Build 204):

* A implementação da API de volume do AdobePSDK.MediaPlayer foi alterada para permitir a reprodução automática no iOS quando a reprodução está sem áudio.

・ Uma nova API, `auditudeSettings.ignoreVPAIDAds`, é adicionado para permitir ignorar anúncios VPAID recebidos do servidor Auditude. A API não funciona para o Fallback do Flash.

**Versão 2.4.11**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.11 do Browser TVSDK:

・ O failover do segmento HLS Live é compatível com os modos de fallback MSE e Flash.

・ Suporte para `AuditudeSettings.creativeRepackagingDomain` A API também está disponível para o MSE. Anteriormente, era compatível somente com o modo de fallback de Flash.

・ A versão contém correções para problemas críticos de clientes. Consulte *Problemas corrigidos* uma lista.

**Versão 2.4.10**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.10 do Browser TVSDK:

・ O TVSDK fornece enableLogging() para ativar ou desativar o registro. Consulte a [Documentação da API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)para uso.

・ O TVSDK não oferece mais suporte a Capítulos padrão ao usar o Adobe Analytics. Defina e gerencie capítulos usando seu aplicativo.

・ A versão contém correções para problemas críticos de clientes. Consulte *Problemas corrigidos *uma lista.

**Versão 2.4.9**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.9 do Browser TVSDK:

・ Fluxos VOD e ao vivo HLS com descontinuidade de tempo, mas sem marcadores de descontinuidade são compatíveis.

・ Os quadros ID3 v2.4.0 são compatíveis com a tag de vídeo Safari para fluxos VOD e ao vivo do HLS.

・ A implementação do carregamento seguro de anúncios garante que as chamadas do servidor de anúncios sejam atualizadas para HTTP seguro com base na configuração da API. Para obter detalhes, consulte AdobePSDK.AdvertisingMetadata e AdobePSDK.ForceHttpsAdConfiguration classes. Este recurso não é compatível com o modo de fallback de Flash.

・ As informações da ID do anúncio e as informações da extensão associadas às respostas do VAST 3.0 agora são disponibilizadas para o aplicativo pelo TVSDK e podem ser usadas para implementar a integração do Mat para medidas do anúncio. Para obter os detalhes, consulte AdobePSDK.NetworkAdInfo API . Isso não é suportado no modo de fallback de Flash.

・ A classe AdobePSDK.ForceHttpsConfiguration não está mais disponível. É bem sucedido por

Classe AdobePSDK.ForceHttpsAdConfiguration.

・ Uma nova API, AdobePSDK.otimizeFlashCalls, está disponível para otimizar as chamadas para melhorar a experiência de reprodução de HLS no modo de fallback do Flash. Isso é desativado por padrão.

**Novo na atualização 2.4.8 (Build 6002)**

Esta atualização contém correções para problemas críticos de clientes. Consulte *Problemas corrigidos*, para a lista.

**Versão 2.4.8**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.8 do Browser TVSDK:

・ O SDK agora é compatível com o Chrome EME e com as alterações de práticas recomendadas disponíveis a partir do Chrome v58. Para obter mais detalhes, consulte [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ A Estrutura da interface do usuário agora suporta o DRM de acesso HLS no Flash, somente anúncios e fluxo de trabalho de informações de direcionamento.

・ A API setDRMAuthenticateData é adicionada à Estrutura da interface do usuário. Para reproduzir fluxos protegidos com DRM de acesso ao Adobe, chame essa API. Como alternativa, o atributo drmAuthenticateData pode ser especificado no player. Consulte [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)para obter detalhes.

**Versão 2.4.7**

Os seguintes recursos são novos na versão 2.4.7:

・ Adição do configurador da interface do usuário na estrutura da interface do usuário

Você pode configurar o reprodutor de uma das seguintes maneiras:

・ Uso de um objeto JSON

・ Uso de APIs

Para ajudar a gerar o objeto JSON, o Browser TVSDK fornece uma ferramenta **UI Configurator **.

Nesta ferramenta, você pode selecionar várias configurações, clicar em **Testar configuração **para verificar as configurações e clicar em **Baixar configuração **para baixar as configurações. Após baixar o arquivo, é possível transmitir o conteúdo desse arquivo como objeto JSON para a API ptp.videoPlayer.

・ Adição da API MediaPlayerItemConfig à estrutura da interface do usuário

Vários recursos, incluindo advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration, podem ser configurados por meio de MediaPlayerItemConfig. Para obter mais informações, consulte a documentação AdobePSDK.MediaPlayerItemConfig no [API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* [documentação](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

Na Estrutura da interface do usuário, a maneira de passar as configurações de rede pela configuração do reprodutor foi modificada.

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

* Suporte para fluxos de trabalho de DRM e Analytics na Estrutura da interface do usuário

As configurações de DRM e o Rastreamento do Analytics podem ser ativados por meio da Estrutura da interface do usuário.

* Adição de `AdobePSDK.embedSWFinFullScreenDiv` API

Essa nova API fornece flexibilidade ao aplicativo do player para selecionar a div na qual ele pode incorporar o arquivo FlashFallback.swf.

* Substituído `getVersion`API de `AdobePSDK.MediaPlayer` classe com `AdobePSDK.Version` classe para informações relacionadas à versão do TVSDK. Para obter detalhes, consulte `AdobePSDK.Version` API [here](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versão 2.4.6**

Os seguintes recursos são novos na versão 2.4.6:

* **Procurar suporte**

A opção Browserify permite usar os módulos de estilo node.js no navegador. Você pode definir as dependências e Procurar agrupa tudo em um arquivo JavaScript.

* **Faturamento**

Com a ajuda do faturamento, o TVSDK do navegador pode coletar métricas de uso do player para faturar clientes do Primetime.

>[!NOTE]
>
>O enum MediaPlayer.Events obsoleto e as constantes obsoletas no Enum PSDKErrorCode foram removidas na versão 2.4.6. Para obter mais informações, consulte [Conversão do Browser TVSDK 2.4.5 para a versão 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versão 2.4.5**

Os seguintes recursos são novos na versão 2.4.5:

* **Reproduções e anúncios completos do evento**

   Os fluxos de Reprodução de evento completo (FER) do HLS agora são compatíveis com a resolução do anúncio e os comportamentos do anúncio. Para ativar esse suporte, defina o modo de sinalização de anúncio como `MANIFEST_CUES` ao criar o `MediaPlayerItemConfig` objeto.

* **Suporte a ScalePolicy MediaplayerView**

   Os desenvolvedores de aplicativos agora podem especificar uma scalePolicy diferente para a exibição usando a propriedade scalePolicy MediaplayerView .

* **Suporte a conteúdo anamórfico**

   A reprodução de conteúdo anamórfico agora é compatível ao usar o MSE e a reprodução do Flash.

* **Aplicação seletiva do`withCredentials`**

When `withCredentials` está definido como verdadeiro, a variável `Access-Control-Allow-Origin` não é possível definir o cabeçalho como curinga. Dependendo da resposta do servidor, o TVSDK do navegador definirá seletivamente a variável `withCredentials` atributo. Para obter mais informações sobre esse suporte, consulte [Documentos da API do TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versão 2.4.4**

Os seguintes recursos foram novos na versão 2.4.4:

* **Aplicativo de amostra do Chromecast**

Esta versão oferece suporte para um aplicativo de remetente e destinatário que demonstra a reprodução de fluxos VOD DASH e fluxos de widevine DASH com inserção de anúncio no lado do cliente.

* **Suporte avançado a failover**

Esta versão contém suporte para casos de uso de failover avançado (failover de segmento e servidor) para fluxos VOD de HLS.

**Versão 2.4.3**

Os seguintes recursos foram novos na versão 2.4.3:

* **Tags personalizadas para VOD DASH**

   Tags personalizadas embutidas (Eventos) podem ser subscritas e recebidas como objeto TimedMetadata.

* **Reprodução de fluxos sem extensões**

   Agora, os fluxos HLS e DASH sem extensões são compatíveis. Para o arquivo manifest, o resourceType precisa ser especificado ao carregar o recurso. Para segmentos e arquivos VTT, o cabeçalho de resposta Content-Type é usado para determinar o tipo de conteúdo.

**Versão 2.4.2**

Os seguintes recursos foram novos na versão 2.4.2:

* **Paridade da API**

Para obter uma lista completa da paridade da API, consulte [TVSDK para DHLS 1.4 para Guia de migração do Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Suporte para AES de exemplo**

   Esta versão adiciona suporte para reprodução de conteúdo criptografado AES de exemplo no fallback de MSE e Flash. O requisito para hospedar conteúdo AES sobre a origem segura no Google Chrome foi removido.

* **Suporte para contêineres AAC**

   A reprodução de arquivos com a extensão .aac agora é compatível. Pode ser apenas áudio ou áudio alternativo.

   >[!NOTE]
   >
   >AC3 e codecs AC3 aprimorados ainda não são compatíveis.

* **Reprodução de fluxo tokenized**

Os fluxos HLS que são entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação nas solicitações de manifesto e segmento para verificação, e esses tokens podem ser fornecidos como parâmetros de URL ou como cabeçalhos de cookies. A reprodução desses fluxos agora é compatível.

**Versão 2.4.1**

Os seguintes recursos foram novos na versão 2.4.1:

* **Estrutura da interface do usuário**

Essa estrutura, projetada para acelerar o desenvolvimento da interface do usuário para aplicativos de player de vídeo baseados em JavaScript, consiste em APIs para incluir controles básicos como reprodução/pausa e volume e para adicionar ou remover facilmente elementos, como estados da barra de depuração e configurações de legenda fechada. Você pode especificar o comportamento associado aos controles, criar controles personalizados e inserir a interface do usuário do reprodutor na pele. Isso tudo acontece por meio da estrutura , sem a necessidade de manipular diretamente a estrutura DOM.

* **Aprimoramentos de reprodução de HLS para fluxos ao vivo**

Esta versão é compatível com descontinuidades causadas pela inserção do anúncio. Ele usa a tag EXT-PROGRAM-DATE-TIME seguida pela tag EXT-MEDIA-SEQUENCE para sincronizar entre perfis de taxa de bits adaptáveis para uma reprodução sem problemas.

* **Suporte a VPAID 2.0**

A definição da interface de veiculação de anúncios do reprodutor de vídeo (VPAID), versão 2.0, oferece uma experiência de mídia avançada para usuários e permite que editores tenham um melhor direcionamento para anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo. Esta versão é compatível com anúncios VPAID lineares do JavaScript para conteúdo de vídeo sob demanda (VOD).

* **Tags HLS personalizadas**

Os fluxos de mídia podem conter metadados adicionais na forma de tags no arquivo playlist/manifest. O TVSDK do navegador permite que você especifique e assine tags adicionais e seja notificado quando essas tags forem exibidas no manifesto.

* **Marcadores de anúncio exibidos na linha do tempo do reprodutor**

Esta versão oferece suporte para mostrar marcadores de anúncio na linha do tempo do reprodutor para conteúdo VOD e ao vivo. Você pode ver esse comportamento no reprodutor de referência.

**Suportado na versão 2.4**

Os seguintes recursos estavam disponíveis na versão 2.4:

* **Reprodução de áudio MP3**

   Esta versão é compatível com a reprodução de áudio MP3 em navegadores com o Media Source Extensions (MSE) e com a tag de vídeo Safari.

* **Reprodução de vídeo MP4**

   Os seguintes recursos são compatíveis:

   * Reprodução de fluxo único
   * Anúncios MP4 antes e depois da exibição com comportamento de anúncios e rastreamento
   * Anúncios HLS antes e depois da exibição com comportamentos de anúncio e rastreamento
   * Anúncios DASH antes e depois da exibição com comportamentos de anúncio e rastreamento

## Plataformas compatíveis {#supported-platforms}

O TVSDK do navegador tem requisitos específicos para os níveis de plataformas e software que ele precisa executar. As seguintes plataformas e níveis de software são suportados:

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

**Google Chromecast (segunda geração; somente para reprodução DASH)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Tecnologia</strong> </p> </td> 
   <td><p><strong>Tag de vídeo TVSDK do navegador</strong><sup>1</sup></p> </td> 
   <td><p><strong>Browser TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>Tecnologia padrão</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>Tag de vídeo</p> </td> 
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
   <td><p>Tag de vídeo</p> </td> 
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
   <td><p>HLS, TRAÇO</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de recursos {#feature-matrix}

Esta é uma lista dos recursos suportados e não suportados para esta versão:

* *Recursos de áudio MP3 — reprodução principal*
* *Recursos de vídeo MP4 — Reprodução principal*
* *Recursos de vídeo MP4 — Ad Insertion principal*

>[!NOTE]
>
>*Nas tabelas de matriz de recursos abaixo, um &quot;Y&quot; significa que o recurso é suportado na versão atual.*

### Recursos de áudio MP3 {#mp-audio-features}

**Quadro 1: Reprodução principal{#table-core-playback}**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD MP3 | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado | Y | Y |

1 A tag de vídeo TVSDK do navegador não suporta streaming e DRM. O suporte a codec e container não é o mesmo em todos os navegadores.

2 O padrão do Firefox é Flash Player para a versão 41 ou anterior.

### Recursos de áudio MP4 {#mp-audio-features-1}

**Quadro 2: Reprodução principal**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD MP4 | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado | Y | Y |

**Quadro 3: Ad Insertion principal**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD MP4 | Antes da exibição (MP4) | Não suportado | Y | Y |
| Ad Insertion | VOD MP4 | Pós-lançamento (MP4) | Não suportado | Y | Y |

Para obter mais informações sobre o suporte a recursos HLS ou DASH, consulte abaixo.

## Matriz de recursos do HLS {#hls-feature-matrix}

Esta é a matriz de recursos para os recursos HLS no Browser TVSDK.

* *Reprodução principal do HLS*
* *Recursos de reprodução avançada HLS*
* *Recursos de proteção de conteúdo do HLS*
* *Recursos de inserção de anúncios do HLS Core*
* *Recursos avançados de inserção de anúncios do HLS*
* *Integrações de HLS*

>[!NOTE]
>
>*Nas tabelas de matriz de recursos abaixo, um &quot;Y&quot; significa que o recurso é suportado na versão atual.*

### Recursos de HLS {#hls-features}

Os seguintes recursos são compatíveis:

**Quadro 4: Reprodução principal do HLS**

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
   <td><p>VOD + Ao vivo</p> </td> 
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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Taxa de bits adaptável</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>608/708 legendas</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Somente VOD</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Failover Manifest</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Failover avançado</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Notificações de QoS e player</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Suporte a QoS limitado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Suporte para cabeçalhos de cookies</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Definindo parâmetros de controle de buffer</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Definir adaptável</p> <p>controles de taxa de bits</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Tags personalizadas</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td>Áudio de ligação tardia</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>302 redirecionamento</p> </td> 
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
   <td><p>Reprodução no offset</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução somente áudio</p> </td> 
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
   <td><p>Tocar com suavização</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Análise do ID3</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Suporte ao marcador de descontinuidade</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Fluxos Tokenized</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Faturamento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 6: Recursos de proteção de conteúdo do HLS**

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>AES de exemplo</p> </td> 
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

**Quadro 7: Recursos de inserção de anúncios do HLS Core**

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Pré-lançamento (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Pós-lançamento (MP4/HLS)</p> </td> 
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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Política de publicidade padrão</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Reembalagem criativa (MP4 para HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 8: Recursos avançados de inserção de anúncios do HLS**

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Parâmetros de direcionamento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Parâmetros personalizados</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Política de anúncio personalizada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Carregamento lento de anúncio</p> </td> 
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

**Quadro 9: Integrações de HLS{#table-hls-integrations}**

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Integração do Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de recursos DASH {#dash-feature-matrix}

Esta é a matriz de recursos para os recursos DASH no Browser TVSDK.

・ ・ *Recursos de reprodução principal DASH*

・ ・ *Recursos de reprodução avançada DASH*

・ ・ *Recursos de proteção de conteúdo DASH*

・ ・ *Recursos de inserção de anúncio principal do DASH*

・ ・ *Recursos avançados de inserção de anúncios do DASH*

・ ・ *Integrações de DASH*

>[!NOTE]
>
>Nas tabelas de matriz de recursos abaixo, um Y significa que o recurso é suportado na versão atual.

### Recursos do DASH {#dash-features}

Os seguintes recursos são compatíveis:

**Quadro 10: Recursos de reprodução principal DASH**

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
   <td><p>VOD + Ao vivo</p> </td> 
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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Taxa de bits adaptável</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>608/708 legendas</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Failover</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Notificações de QoS e player</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Suporte para cabeçalhos de cookies</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Definindo parâmetros de controle de buffer</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Definir controles adaptáveis da taxa de bits</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Tags personalizadas (EventStream)</p> </td> 
   <td><p>Somente VOD (em linha)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Áudio de ligação tardia</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>302 redirecionamento</p> </td> 
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
   <td><p>Reprodução no offset</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Reprodução somente áudio</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick Play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Tocar com suavização</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Análise do ID3</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Suporte a vários períodos</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Fluxos Tokenized</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Faturamento</p> </td> 
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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>AES de exemplo</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Widevine no Chrome, Firefox 47 e posterior e Chromecast</p> <p>・ PlayReady no Internet Explorer no Windows 8.1 e Edge</p> <p>・ DRM do Primetime para Windows Firefox (somente vídeo)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 13: Recursos de inserção de anúncio principal do DASH**

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Antes da exibição (MP4/DASH)</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Pós-lançamento (MP4/DASH)</p> </td> 
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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Política de publicidade padrão</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
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
   <td><p>Parâmetros de direcionamento</p> </td> 
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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Política de anúncio personalizada</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Carregamento lento de anúncio</p> </td> 
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

**Quadro 15: Integrações de DASH**

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Integração do Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemas corrigidos {#issues-fixed}

**Problemas corrigidos na atualização 2.4.12 (Build 204)**

Os seguintes problemas foram corrigidos na Atualização 2.4.12 do Browser TVSDK (Build 204):

・ ・ **21647**- O TVSDK deve permitir a reprodução automática de vídeo em dispositivos iOS quando o áudio estiver sem áudio.

・ ・ **21465**- Error Key System Access Denied (Acesso negado ao sistema de chave de erro é recebido ao reproduzir um fluxo DASH protegido por DRM depois que um fluxo DASH Live é reproduzido.

・ ・ **21442**- Ative a reprodução automática de conteúdo no iOS Web, após a reprodução do anúncio de pré-lançamento com um gesto de usuário.

・ ・ **21240**- API fornecida para filtrar anúncios VPAID analisados do Auditude/VMAP.

**Problemas corrigidos na versão 2.4.11**

Os seguintes problemas foram corrigidos no Browser TVSDK versão 2.4.11:

**Recursos da reprodução principal:**

・ ・ **19192**: O TVSDK agora implementa TextFormat:bottomInset e TextFormat:safeArea. Devido a esses aprimoramentos, as legendas ocultas podem ser reposicionadas se a barra de controle for exibida na tela.

・ ・ **21009**: As legendas ocultas persistem na tela em caso de descontinuidade até que novas legendas sejam exibidas.

・ ・ **21141**: A busca de retorno é rejeitada devido a uma condição de corrida durante a anexação do segmento.

・ ・ **21142**: Disponibilizar intervalos de reprodução pesquisáveis quando o reprodutor estiver no estado INICIALIZADO. Devido a essas alterações, a sessão de início na posição agora é suportada.

・ ・ **21363**: As legendas ocultas 608/708 estão fora de sincronia após a inserção do anúncio para os fluxos DASH.

**Recursos de inserção de anúncio:**

・ ・ **21179**: Problemas relacionados ao mid-roll (pausas longas, quadros pretos) com conteúdo VOD agora são resolvidos definindo corretamente a propriedade ad.primaryAsset.adParameters .

・ ・ **21257**: O arquivo MP4 com a maior taxa de bits é selecionado para transcodificação se MP4 não for um tipo MIME válido e o recurso de reempacotamento criativo estiver ativado.

・ ・ **21361**: O TVSDK agora passa o sistema de anúncios e a ID criativa da resposta do VAST como parâmetros de consulta na solicitação do pacote criativo para oferecer suporte a regras de normalização adicionais.

**Problemas corrigidos na versão 2.4.10**

Os seguintes problemas foram corrigidos no Browser TVSDK versão 2.4.10:

**Recursos da reprodução principal:**

・ ・ **21060**: Erro de codec inválido lançado com fluxos HLS que contêm descontinuidade e as caixas BMFF ISO são executadas até o fim do fluxo.

・ ・ **21045**: A reprodução automática não funciona no iOS após a conclusão da primeira reprodução de vídeo em uma lista de reprodução.

・ ・ **20975**: A taxa de quadros é retornada como NaN pelo provedor de QoS no navegador Chrome.

・ ・ **20823**: Erro de codec não suportado lançado ao encontrar segmentos sem dados.

・ ・ **20769**: O SDK agora inicia com a taxa de bits atual em busca, em vez de alternar imediatamente com base na política ABR.

・ ・ **20031**: Quando no modo retrato do IE11 (Windows 8.1), a tela de vídeo fica pequena. Recurso de proteção de conteúdo:

・ ・ **19316**: Ignorar segmentos que falham na descriptografia no caso de fluxos AES-128 HLS.

**Problemas corrigidos na versão 2.4.9**

Os seguintes problemas foram corrigidos no Browser TVSDK versão 2.4.9:

**Recursos da reprodução principal:**

・ ・ **13407**: Os fluxos DASH podem ser interrompidos se o Firefox parar de enviar o evento &quot;ontimeupdate&quot; durante a reprodução.

・ ・ **16380**: Durante a reprodução do conteúdo de vídeo de áudio muxed, de segmentos com horários de início não correspondentes via MSE, o Erro de sincronização de áudio entre representações é acumulado em switches ABR, resultando em Erro (problema de Chromium #663686).

・ ・ **17985**: Ao reproduzir um fluxo ISO-BMFF específico no navegador Firefox, a reprodução fica travada (problema do Firefox nº 1342913). Isso é corrigido desde o Firefox v53.

・ ・ **1914**: ReferenceError não captado (em promessa): largura não está definida.

・ ・ **1897, 19299**: Problema de cintilação de vídeo no limite do segmento. Isso ocorria, pois o SDK não calculava o deslocamento de tempo de Composição da última amostra corretamente.

・ ・ **19780**: A reprodução não é iniciada para conteúdo HLS e anúncio HLS no Firefox v53 (problema do Firefox nº 354653).

・ ・ **20046**: A Data e Hora do Programa é recebida como chave em vez de valor quando recebida como objeto de metadados cronometrados.

・ ・ **2004**: useDefaultResizeHandler gera um erro com o fallback do Flash.

・ ・ **2017**: Fallback do Flash não funciona com Flash Player v25.0.0.171.

・ ・ **20293**: O Firefox interrompe os dados de buffering para determinados fluxos de HLS, levando à paralisação.

・ ・ **20626**: O reprodutor gera um erro de decodificação de mídia no Chrome devido ao tratamento incorreto de amostras de vídeo com duração zero.

・ ・ **20078**: A reprodução é interrompida no erro de navegador &#39;QuotaExcedido&#39;.

・ ・ **18639**: No HLS Live stream 608 CC, o texto às vezes aparece como ortografia incorreta.

・ ・ **20028**: O parâmetro de tamanho ClosedCaptions não altera o tamanho da fonte.

・ ・ **20613**: As caixas de legendas ocultas se sobrepõem umas às outras, tornando-as ilegíveis.

**Recursos do Ad Insertion principal (CSAI):**

・ ・ **20043**: Impressão de anúncio ausente e chamadas de rastreamento de anúncios com vários anúncios e redirecionamentos de terceiros.

・ ・ **2004**: Ao usar o reempacotamento criativo, todos os anúncios no ad break precisam ser reempacotados com êxito, caso contrário, o ad break é completamente descartado.

・ ・ **20097**: A reprodução do anúncio é ignorada e o conteúdo principal é retomado imediatamente, em vez de aguardar o tempo limite de 20 segundos se o manifesto do anúncio não estiver disponível.

**Problemas corrigidos na atualização da versão 2.4.8 (Build 6002)**

Os seguintes problemas foram corrigidos na Atualização do Browser TVSDK versão 2.4.8 (Build 6002):

・ ・ **14126:** A reprodução pode ser interrompida no Firefox (edição nº 1316024) devido a uma lacuna interna no buffer de origem MSE. Tente buscar para retomar a reprodução

・ ・ **19608:** Correção para honrar o valor de deslocamento de tempo da resposta do VMAP do Auditude.

・ ・ **19635:** Corrige a paralisação de vídeo no Internet Explorer 11 no Windows 10.

・ ・ **19761:** Correções para problemas de ABR com HLS.

・ ・ **19780:** Corrige a reprodução do anúncio com conteúdo HLS que foi quebrado no Mozilla Firefox v53.

・ ・ **1987 e 1974:** Os problemas corrigem a inconsistência na seleção da taxa de bits após uma operação de busca. Agora, a seleção da taxa de bits na busca é o valor mais baixo da taxa de bits atual e da taxa de bits na inicialização.

・ ・ **19881:** A reprodução travada e a sobreposição de buffering aparece por tempo infinito após a busca ser executada por 3 a 4 vezes.

・ ・ **19884:** Confirme a conformidade com os requisitos do Chrome 59 Beta Verified Media Path (VMP). O bTVSDK foi capaz de reproduzir o conteúdo de DRM da Widevine com o Chrome 59 Beta.

・ ・ **19916:** A reprodução de DRM na estrutura da interface do usuário foi interrompida. Agora, chama acquisitionLicense mesmo se não houver uma política nos metadados.

**Problemas corrigidos na versão 2.4.8**

Os seguintes problemas foram corrigidos na versão 2.4.8 do Browser TVSDK:

・ ・ **10075**: Ao buscar antes da linha do tempo, o evento de conclusão de reprodução não foi recebido no Firefox e no Chrome e o evento de busca não foi recebido no Firefox.

・ ・ **15775**: Reproduzir evento concluído não recebido no Windows 8.1 Internet Explorer.

・ ・ **17306**: Para fluxos SSAI, a reprodução é compatível. O rastreamento de anúncios compilados não é suportado.

・ ・ **19142**: Às vezes, o retrocesso faz com que o reprodutor de vídeo permaneça no estado de buffer para sempre.

・ ・ **19218**: Os marcadores de anúncios não estão disponíveis por meio da estrutura da interface do usuário.

・ ・ **19.219**: A reprodução de anúncios só não funciona pela estrutura da interface do usuário.

・ ・ **1922**: A chave AES-128 é solicitada uma vez para uma lista de reprodução e as solicitações subsequentes são atendidas a partir do cache. Anteriormente, era solicitado para cada segmento.

・ ・ **19597**: &quot;TypeError não captado: Não é possível ler a propriedade &quot;log&quot; de indefinido&quot; foi vista com compilações de canário do Chrome.

・ ・ **19605**: adRequestDomain não estava disponível no modo Fallback de Flash.

・ ・ **19608**: Anúncios VMAP não estavam sendo inseridos para fluxos HLS ao vivo. O SDK agora considera os marcadores de sinalização e não depende dos valores de deslocamento de tempo nas respostas do VMAP.

・ ・ **19637**: Somente a reprodução de anúncios resulta em erro de script no fim do anúncio.

・ ・ **19732**: As solicitações da lista de reprodução do CRS falhavam com o erro 404. As solicitações 1401 e 1403 do Browser TVSDK foram atualizadas para resolver isso.

・ ・ **19762**: acquisitionLicense costumava ser chamado antes de setAuthenticationToken por causa do qual uma licença válida era retornada, independentemente da validade do token. Isso foi corrigido agora e o acquisitionLicense é chamado somente após a resposta de setAuthenticationToken.

**Problemas corrigidos na versão 2.4.7**

Os seguintes problemas foram corrigidos na versão 2.4.7:

・ ・ **8397**: Os fluxos ao vivo do HLS gerados pelo Adobe Medium Server podem não ser reproduzidos se os segmentos não começarem com um quadro Chave.

・ ・ **13606**: Vários problemas relacionados à Busca foram corrigidos para o fluxo de HLS no navegador Chrome.

・ ・ **14807**: No navegador Chrome, se a busca ou pausa for acionada imediatamente após play(), a reprodução pode parar com o erro DOMException: A solicitação play() foi interrompida por uma chamada ...(Chromium número 593273).

・ ・ **19085**: Os parâmetros do MediaPlayer, como volume, abrControlParameters e ccStyle, não são definidos como Padrões na redefinição do reprodutor.

**Problemas corrigidos na versão 2.4.6**

O seguinte problema foi corrigido na versão 2.4.6:

・ ・ **18093**: TimedMetadata para a tag ao lado da tag subscrita é retornado quando você usa a versão 24 do Flash Player no modo Fallback do Flash.

**Problemas corrigidos na versão 2.4.4**

Os seguintes problemas foram corrigidos na versão 2.4.4:

・ ・ **8711**: Com o MSE, as legendas 608/708 são justificadas por padrão.

・ ・ **13934**: As configurações ABR para anúncios não são aplicáveis ao reproduzir com fluxos ao vivo do HLS.

・ ・ **14079**: A longevidade de fluxos HLS ao vivo com uma janela de DVR baixa pode falhar, pois a reprodução pode ficar para trás devido a problemas de latência de rede. Clique no ponto ativo para retomar a reprodução.

・ ・ **15037**: As amostras fornecidas com a estrutura da interface do usuário do reprodutor não funcionam no Microsoft Internet Explorer 10 no Windows 7.

・ ・ **15913**: Para fluxos VOD de HLS, no Chrome, o fluxo não será reproduzido se a resposta do manifesto não for 304 modificada. Isso é corrigido desde o Chrome v55 (Chromium issue 633696).

・ ・ **16103**: No Android Chrome, em condições de pouca largura de banda, a reprodução pode parar com o TypeError não captado: Não é possível ler a propriedade &#39;programDateTime&#39; do erro indefinido.

・ ・ **16265**: Para fluxos VOD e ao vivo do HLS, a busca por descontinuidades não funciona.

・ ・ **16709**: Retomar o fluxo ao vivo do HLS com PDT e o marcador de descontinuidade podem levar o reprodutor a ficar preso no buffer.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

As limitações e os problemas conhecidos no TVSDK do navegador são mencionados abaixo.

**Quadro 16: Recursos principais da reprodução**

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
   <td>VOD + Ao vivo</td> 
   <td>Reprodução geral (Reproduzir, Pausar, Buscar)</td> 
   <td><p>・ Não há suporte para formatos de mídia diferentes de HLS.</p> <p>8799: O fallback do Flash não cuida de conteúdo misto e, portanto, é necessário garantir que Conteúdo, Publicidade e outros URLs não levem a conteúdo misto (conteúdo seguro e inseguro juntos).</p> <p>19271: A reprodução de várias visualizações por meio da estrutura da interface do usuário não é compatível com o modo de fallback de Flash.</p> <p>・ O fallback do Flash não funciona no Microsoft Internet Explorer 8 e 9 no Windows 7, pois essas versões não são compatíveis com o SDK.</p> <p>20262: O fallback do Flash adiciona parâmetros personalizados à lista de informações de direcionamento. Além disso, a ordem de prioridade dos parâmetros personalizados é diferente no caso de Flash e MSE.</p> <p>・ 20653:O fallback do Flash TVSDK do navegador não funciona no Win10 com a Atualização de criadores.</p> <p>・ O Fallback do Flash funciona com o Flash Player versão 23 e posterior.</p> <p>・ 20087 - Chrome 59 Beta com</p> <p>Flash 25.0.0.171</p> <p>Beta(padrão), a reprodução de HLS não está funcionando no modo de Fallback do Flash. Está funcionando bem em Canário.</p> </td> 
   <td><p>12563: Os Dash Streams com codec de áudio mp4a.40.02 não são reproduzidos no Firefox devido à sequência de codec de áudio não suportada no MPD. O Codec de áudio mp4a.40.2 é compatível.</p> <p>15029: Ao alternar entre vídeos no multiView na Estrutura da interface do usuário, o botão Reproduzir/pausar não é atualizado adequadamente.</p> <p>・ 16034:No IE do Windows 8.1, chamar reset() leva a um erro de tipo MIME desconhecido. Recarregue a mídia para retomar a reprodução.</p> <p>18235: Certos problemas de busca são observados com fluxos de vod DASH com anúncios.</p> <p>18727: A API de erro não é compatível com o MSE</p> <p>18750: Os eventos de Alteração de status podem estar fora de ordem em alguns casos para a estrutura do SDK e da interface do usuário e, na Estrutura da interface do usuário, os eventos de IDLE e Inicialização do StatusChange podem estar ausentes para os ouvintes de eventos adicionados após o carregamento do recurso.</p> <p>18889: Se MediaPlayer estiver em estado ERROR, o objeto view não será retornado.</p> <p>19039: Se o AdobePSDK. MediaPlayer. searchToLocal() é usado com um valor maior que EOF, então a reprodução começa do início no caso de MSE.</p> <p>19049: Nenhum estado de erro relatado para o Flash Player no Chrome, IE, Firefox quando o vídeo é bloqueado durante a reprodução.</p> <p>17205: A reprodução de vídeo é interrompida ao reproduzir fluxo sem mudo por algumas horas enquanto o áudio continua a ser reproduzido (problema Chromium# 664033).</p> <p>12308: Fluxos DASH com a composição_ time_offset especificada podem ter timeStampOffset aplicado a ele no navegador Chrome, levando ao tempo de decodificação negativo e, portanto, ao erro MEDIA_ERR_ SRC_NOT_ SUPPORTED (problema Chromium #398141).</p> <p>14126: A reprodução pode ser interrompida no Firefox (número de edição 1316024) devido a uma lacuna interna no buffer de origem MSE. Tente buscar para retomar a reprodução.</p> <p>19115: O MS Edge e o IE 11 (Win 8.1 e 10) não definem a Origem como nula no redirecionamento do CORS e ainda falham porque o cabeçalho não é nulo, resultando em erro de reprodução.</p> <p>・ 19861:Problema com o comportamento de anexação no buffer de origem para mídia já reproduzida. O Chrome rejeita o fragmento anexado, incluindo moov, causando erro de decodificação subsequente. (Problema de crômio nº 735335)</p> <p>19921: A reprodução é interrompida para determinado conteúdo HLS, mesmo com seu buffer bem-sucedido (problema de Chromium #713540)</p> <p>2044:A busca do fim do intervalo em buffer no IE e no Edge pode fazer com que a reprodução seja interrompida.</p> <p>20511: Às vezes, a busca de rejeição pode ser observada para fluxos HLS com ou sem anúncios.</p> <p>20743: No Windows 10 Chrome, o fluxo do HLS Live é reproduzido por alguns segundos antes da reprodução do MP4 precedente.</p> <p>21043: A dimensão Vídeo pode não estar correta no carregamento inicial devido à falta de metadados.</p> <p>21115: O gesto do usuário do Android é necessário para iniciar a reprodução se o anúncio precedente estiver disponível para vídeos em uma lista de reprodução.</p> <p>・ HLS Live não suporta a sobreposição do carimbo de data/hora.</p> <p>・ Não há suporte para áudio AAC-SSR.</p> <p>Os codecs de áudio AC3 e AC3 aprimorado não são compatíveis.</p> <p>・ Para fluxos com descontinuidade de carimbo de data e hora, mas sem marcadores de descontinuidade</p> <p>・ A reprodução pode ter falhas e busca incorreta devido a saltos.</p> <p>・ A duração do conteúdo e a duração da reprodução podem não corresponder.</p> <p>・ As descontinuidades entre representações e representações devem corresponder a outros tipos de sensatez pode levar a problemas de sincronização e paralisação.</p> <p>・ As legendas e a WebVTT podem não aparecer perto do fim do fluxo.</p> <p>・ As alterações no codec de áudio não são suportadas em saltos de carimbo de data e hora.</p> <p>・ A inserção de anúncio não é suportada.</p> <p>・ O modo de truque avançado pode levar ao loop de reprodução no Win 8.1 IE 11 (problema MS nº 12446268).</p> <p>TRAÇO:</p> <p>・ Para fluxos ao vivo - o perfil ao vivo com tipo dinâmico é suportado.</p> <p>・ Para fluxos VoD - o perfil dinâmico com tipo estático é suportado.</p> <p>Para fluxos de VoD - o perfil sob demanda não é certificado para fluxos de trabalho de anúncios.</p> </td> 
   <td><p>・ Os fluxos DASH Live e DASH Video on Demand não são suportados.</p> <p>・ A reprodução de vídeo PIP(Picture in Picture) não é compatível com o iOS no modo de tela cheia.</p> <p>Na extensão Safari (Tag de vídeo), menos manifesto sem ter o cabeçalho de tipo de conteúdo correto não funciona.</p> </td> 
   <td><p>・ O applicationID no aplicativo do remetente precisa ser o mesmo gerado no registro do URL do Destinatário como um aplicativo do Destinatário personalizado.</p> <p>・ O reprodutor de referência é certificado para workflows DASH. A estrutura da interface do usuário não está certificada.</p> <p>Para obter a lista de codecs de mídia compatíveis, consulte <a href="https://developers.google.com/cast/docs/media"><em>here</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Reprodução geral (Reproduzir, Pausar, Buscar)</td> 
   <td> </td> 
   <td>18098: Certos problemas de busca são observados com o fluxo de FER do LBA HLS.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Taxa de bits adaptável</td> 
   <td><p>・ 20079: Regravação de buffer em busca dentro do intervalo em buffer.</p> <p>20080: O comportamento ABR do Flash é consistente com o MSE.</p> </td> 
   <td><p>・ A variante de fallback somente de áudio em um fluxo ABR é ignorada devido a limitações relacionadas ao buffer.</p> <p>12289: Os parâmetros de controle ABR não se aplicam ao áudio no caso de fluxos HLS/DASH sem mudo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>608/708 Legendas</td> 
   <td> </td> 
   <td><p>7810: No Android 4.4.4, o Chrome não parece ter suporte para famílias básicas de fontes CSS usadas pelo reprodutor e, portanto, a função de alteração do estilo de fonte não está funcionando.</p> <p>・ Os canais CC não podem ser alterados no caso de 608 legendas.</p> <p>・ Os recursos avançados de estilo não são compatíveis com legendas 608.</p> <p>Legendas incorporadas (608/708), sinalizadas por meio de tags de Acessibilidade são compatíveis.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>5206: As tags de região no arquivo WebVTT são ignoradas pelo reprodutor ao exibir as legendas.</p> <p>DASH: Arquivos VTT fragmentados /Segmentados não são compatíveis.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Failover manifest</td> 
   <td>21056: Com o Fallback de Flash, o Failover não ocorre para o Live Stream se o stream principal retornar um erro 404 durante a reprodução.</td> 
   <td>O failover de manifesto é aplicável somente para conteúdo e não para anúncios.</td> 
   <td>O failover da lista de reprodução ausente funciona no Safari somente para o código de erro HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Failover avançado</td> 
   <td> </td> 
   <td><p>・ O failover de segmento não oferece suporte para ignorar segmentos indisponíveis e continuar a reprodução.</p> <p>20533: Segmentos ausentes em uma lista de reprodução devem ser tratados como Descontinuidade e a reprodução deve retomar do próximo segmento disponível.</p> <p>21267: A alternância de fluxo devido a failover pode levar ao download de segmentos mais antigos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Notificações de QoS e Player</td> 
   <td>21129: A taxa de quadros não está disponível no caso de Fallback de Flash.</td> 
   <td><p>11170:</p> <p>O Timed_Event não está disponível para o Browser TVSDK com MSE, ao contrário do Browser TVSDK com Flash Fallback.</p> <p>21129: A taxa de quadros não é calculada para fluxos ao vivo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Suporte para cabeçalhos de cookies</td> 
   <td> </td> 
   <td> </td> 
   <td><p>O sinalizador withCredentials e os cabeçalhos de cookies não são compatíveis com o Safari.</p> <p>21051: Para permitir cookies no Safari, ative a configuração "Cookies e dados do site" em Preferências &gt; Privacidade.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Tags personalizadas</td> 
   <td>14763: Tags personalizadas diferentes de iniciar com # não devem ser suportadas. No momento, o objeto TimedMetadata é criado e relatado para essas tags durante o Fallback do Flash.</td> 
   <td>Os fluxos com tags personalizadas em banda não são certificados.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Áudio de ligação tardia</td> 
   <td> </td> 
   <td><p>・ A inserção de anúncio não é compatível com fluxos HLS Live LBA.</p> <p>17273: Os fluxos de LBA VOD do HLS mudam para a representação padrão em caso de failover e não podem ser retornados para a última seleção.</p> <p>20251: O fluxo do LBA Live do HLS pode ficar parado na busca.</p> <p>20497: O player permanece no estado de buffering se os fluxos sem mudo LBA de HLS tiverem quadros de áudio ou vídeo ausentes próximos ao fim do fluxo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>302 Redirecionamento</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>a otimização de redirecionamento não é compatível com os navegadores Windows Edge e IE, pois eles não suportam a propriedade responseURL no objeto XMLHttpRequest .</p> </td> 
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
   <td>Reprodução no offset</td> 
   <td><p>Iniciar a reprodução em um valor de deslocamento específico não é compatível com o conteúdo MP4.</p> </td> 
   <td>20492: Anúncios intermediários antes do deslocamento são reproduzidos antes que o conteúdo retome do valor do deslocamento.</td> 
   <td>A reprodução com recurso de deslocamento não é compatível com o iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>O Tocar suave não funciona para fluxos sem representações de iFrame.</td> 
   <td><p>・ As adaptações do Trick Play não são compatíveis com o Firefox e o Internet Explorer e, portanto, o modo de truque reverso não está disponível nesses navegadores.</p> <p>・ O Trickplay não está disponível ao reproduzir conteúdo junto com anúncios.</p> <p>10435: Durante a reprodução do DASH, o vídeo congela durante a reprodução de truques avançados no Internet Explorer (Win 8.1)</p> <p>intermitentemente. Isso ocorre porque estamos usando a propriedade playbackRate dos elementos de vídeo sem a adaptação da reprodução de truques.</p> <p>14182: Às vezes, durante o rebobinamento no navegador Chrome, o evento de busca pode não ser recebido e, portanto, o modo de truques não funcionará.</p> <p>14942: As taxas de reprodução podem ser definidas no Chrome para Android, mesmo no caso de fluxos de reprodução sem engano, mas a configuração não será aplicada e a reprodução continuará em uma taxa normal.</p> <p>17308: A busca não funciona no modo Trickplay.</p> <p>17309: No navegador Chrome, o modo de truque reverso não pode ser mantido por mais de 2 segundos.</p> <p>19272: A reprodução de truque pode não se recuperar do buffering no navegador Windows 10 Edge no caso de fluxos DASH.</p> </td> 
   <td>O modo de truque de retrocesso não é suportado.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Análise do ID3</td> 
   <td>20346: O byte de codificação de texto de quadros ID3 também deve ser retornado pelo SDK.</td> 
   <td><p>As tags ID3 disponíveis em fluxos de transporte de dados de áudio (ADTS) são ignoradas pelo SDK.</p> <p>12378: Os metadados cronometrados de ID3 são analisados em momentos diferentes no Flash e no navegador com suporte a MSE e, portanto, o comportamento de exibição na linha do tempo do reprodutor de referência também é diferente.</p> <p>19247: A análise de ID3 não é compatível com a estrutura da interface do usuário.</p> </td> 
   <td><p>20323: A tag PRIV ID3 usada para sinalizar o carimbo de data e hora da primeira amostra de segmento aac não é analisada pelo Safari (problema do Safari nº 32422733)</p> <p>20350: Em determinados dispositivos (incluindo o MAC OS X 10.1, iPad10), o Safari não fornece evento de alteração de sinalização quando em modo de truque e, portanto, os quadros ID3 não são recebidos. (Problema do Safari #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Suporte ao marcador de descontinuidade</td> 
   <td> </td> 
   <td><p>・ A inserção de anúncio do lado do cliente não é compatível com fluxos HLS contendo descontinuidade.</p> <p>・ A alteração do codec de áudio não é permitida em descontinuidades no fluxo de HLS.</p> <p>・ O switch de faixa de áudio não é compatível com fluxo de HLS com marcadores de descontinuidade</p> </td> 
   <td>O número de sequência de descontinuidade é um requisito para fluxos HLS com descontinuidade para reprodução no Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 18: Recursos da proteção de conteúdo**

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
   <td>VOD + Ao vivo</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>O intervalo de bytes não é suportado com conteúdo criptografado AES-128.</td> 
   <td>12324: Os fluxos criptografados AES-128 do HLS falham na reprodução no Safari se a tag IV não estiver especificada.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>12660: O reprodutor HTML5 lança Erro Interno do Servidor para conteúdo de traço criptografado PlayReady expirado.</p> <p>16720: O conteúdo criptografado por DASH DRM não funcionará se o atributo de início na tag de período estiver ausente.</p> <p>18589: A reprodução não é compatível com fluxos DRM VoD de vários períodos protegidos por DRM com Xlink.</p> <p>18653: A reprodução do conteúdo widevine de vários períodos com várias chaves é interrompida no primeiro período e não pode alternar para o próximo.</p> <p>18656: Playready MultiPeriod Stream, criptografado com chaves diferentes, não reproduzirá.</p> <p>O Playready 2.0 para Dash não está certificado.</p> <p> </p> <p> </p> </td> 
   <td>12602: Metadados DRM HLS Fairplay são atualizados repetidamente pelo reprodutor HTML5 no Safari</td> 
   <td><p>É possível reproduzir o conteúdo DRM da widevina DASH empacotado por meio do Bento4. O conteúdo empacotado pelo Offline Packager e pelo Shaka Packager não é reproduzido. O DRM DASH PlayReady não é suportado.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 19: Recursos do Ad Insertion principal (CSAI)**

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
   <td>VOD + Ao vivo</td> 
   <td>Pré/média/publicação</td> 
   <td> </td> 
   <td><p>・ Os anúncios precedentes com conteúdo HLS ao vivo são reproduzidos no modo de reprodução dupla.</p> <p>・ Anúncios DASH com conteúdo HLS e anúncios HLS com conteúdo DASH não são compatíveis.</p> <p>19002: No HTML5 Player com MSE adBreak. insertionType não retorna o valor correto para descrever o tipo de inserção correto, ou seja, o cliente foi inserido e ou o servidor foi inserido.</p> <p>7794: Em dispositivos móveis (iOS, Android com Chrome 33 ou navegador inferior ou nativo) onde a barra de controle padrão é visível no modo de tela cheia, a barra de busca e os botões para frente rápidos estão disponíveis quando a Reprodução de anúncios.</p> <p>11048: Alternar de anúncio para conteúdo HLS Live não é suave no caso de Extensões de fonte de mídia.</p> <p>16083: No Android 4.4 Chrome v52, às vezes o anúncio do HLS com conteúdo HLS pode levar a um erro de decodificação de pipeline após a reprodução paralisada.</p> <p>16097: Os erros encontrados durante o Ad break não são tratados, pode fazer com que o fluxo principal pare a reprodução.</p> <p>18095: Anúncios MP4 não são compatíveis com conteúdo HLS ao vivo.</p> <p>19120: Várias buscas em anúncios HLS com conteúdo HLS podem fazer com que o fluxo pare a reprodução.</p> <p>19131: A sobreposição de buffer pode aparecer ao alternar do ad break precedente para o conteúdo.</p> <p>20296: No caso de fluxos ao vivo do HLS, a busca de volta na janela DVR seguida pela busca em rolos intermediários resolvidos pode levar à paralisação da reprodução.</p> <p>・ 20298:HLS Live streams com rolls intermediários paralisam o momento em que o lançamento é iniciado e se move para fora da janela DVR.</p> <p>20317: Os fluxos ao vivo do HLS podem ser interrompidos ao alternar para o próximo anúncio ou de anúncio para conteúdo, caso o ad break contenha mais de um anúncio.</p> 
    <ul> 
     <li>Os anúncios na janela do DVR de fluxos do HLS Live não são resolvidos.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>O SDK não respeita o atributo de sequência dentro da resposta VMAP para VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: O SDK não respeita o atributo de sequência dentro da resposta VMAP para VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: O atributo de repetição VMAP não é suportado.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Reembalagem criativa</td> 
   <td> </td> 
   <td>21464: A resposta do anúncio é totalmente descartada se o reempacotamento criativo falhar em um dos anúncios no ad break.</td> 
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
   <td>VOD + Ao vivo</td> 
   <td>Política de anúncio personalizada</td> 
   <td> </td> 
   <td><p>・ Comportamentos de anúncios não são compatíveis com anúncios MP4 e conteúdo MP4.</p> <p>13973: Comportamentos de anúncio personalizados - A política de SKIP não lança um evento completo quando usada com MSE.</p> <p>14939: As políticas personalizadas de comportamento de anúncio ignoradas e ignoradas não funcionam para o conteúdo DASH.</p> <p>17131: O primeiro quadro do anúncio é visível e, em seguida, o conteúdo é retomado no caso de política de interrupção de anúncio IGNORADA.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Anúncios complementares/anúncios de banner/ anúncios clicáveis</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Anúncios de banner não são visíveis ao usar o reprodutor de referência.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ Comportamentos de anúncio não são compatíveis com anúncios VPAID.</p> <p>15032: Anúncios VPAID em combinação com anúncios MP4 ou HLS em um ad break não são compatíveis.</p> <p>19001: No Android e no iOS, quando o anúncio VPAID é reproduzido com MP4 como o conteúdo principal, as trilhas duplas de áudio são audíveis, um do conteúdo principal e um do anúncio.</p> <p>20762: Anúncios VPAID não são compatíveis com o Picture in Picture (PIP).</p> <p>21172: O evento Reproduzir concluído não é recebido para conteúdo VOD HLS com anúncios VPAID.</p> <p>21173: onAdBreakCompleteEvent não é recebido para conteúdo de VOD HLS e anúncios VPAID pós-roll.</p> </td> 
   <td>O reprodutor alterna entre o modo normal e o modo de tela cheia ao alternar entre VPAID e conteúdo principal.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Quadro 21: Integrações**

| **Tipo de conteúdo** | **Recurso** | **Flash** | **HTML5 no Firefox, IE, Chrome, Android Chrome** | **HTML5 no Safari, iOS Safari** | **Chromecast (apenas reprodução DASH)** |
|---|---|---|---|---|---|
| VOD + Ao vivo | Integração do Adobe Analytics VHL |  | 1904: O rastreamento do Video Analytics não está disponível por meio da ferramenta de configuração de interface do usuário. |  |  |

## Recursos úteis {#helpful-resources}

* Consulte a documentação completa de ajuda em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
