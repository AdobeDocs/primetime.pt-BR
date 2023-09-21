---
title: Notas de versão do TVSDK 2.4 do navegador
description: As Notas de versão do TVSDK 2.4 do navegador descrevem os recursos novos, compatíveis e não compatíveis, e os problemas conhecidos no TVSDK 2.4 do navegador.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Notas de versão do TVSDK 2.4 do navegador {#browser-tvsdk-release-notes}

As Notas de versão do TVSDK 2.4 do navegador descrevem os recursos novos, compatíveis e não compatíveis, e os problemas conhecidos no TVSDK 2.4 do navegador.

## Introdução {#introduction}

O TVSDK do navegador é um kit de ferramentas que permite adicionar funcionalidade avançada de reprodução de vídeo, proteção de conteúdo e publicidade aos aplicativos de player de vídeo baseados no navegador.

O TVSDK 2.4 do navegador fornece APIs JavaScript para criar aplicativos de vídeo baseados em navegador e inclui suporte para reprodução nos seguintes modos:

* Somente HTML5
* HTML5 com fallback de flash automático
* Flash sempre

Esta versão inclui as seguintes informações:

· [Documentação da API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [Guia de programação do TVSDK do navegador](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [Guia de migração do TVSDK para DHLS 1.4 para Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [Conversão do TVSDK 2.4.6 do navegador para a versão 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

· Uma implementação de referência, que está incluída na build.

>[!NOTE]
>
>*Para obter uma lista completa das considerações de segurança para esta versão, consulte Considerações de segurança.

## Novidades e recursos compatíveis {#what-s-new-and-supported-features}

Esta versão do TVSDK para navegador fornece novos recursos que você pode usar para aprimorar seus aplicativos de vídeo.

**Novidade na Atualização 2.4.12 (Build 204)**

A seguinte adição está disponível como parte da Atualização do TVSDK 2.4.12 do navegador (Build 204):

* A implementação da API de volume do AdobePSDK.MediaPlayer é alterada para permitir a reprodução automática no iOS quando a reprodução estiver sem áudio.

· Uma nova API, `auditudeSettings.ignoreVPAIDAds`, é adicionado para permitir ignorar anúncios VPAID recebidos do servidor Auditude. A API não funciona para o fallback do Flash.

**Versão 2.4.11**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.11 do TVSDK do navegador:

· O failover de segmento HLS Live é compatível com os modos de fallback MSE e Flash.

· Suporte para `AuditudeSettings.creativeRepackagingDomain` A API agora também está disponível para o MSE. Anteriormente, só era compatível com o modo de fallback do Flash.

· A versão contém correções para problemas críticos do cliente. Consulte *Problemas corrigidos* uma lista.

**Versão 2.4.10**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.10 do TVSDK do navegador:

· O TVSDK fornece enableLogging() para ativar ou desativar o registro. Consulte a [Documentação da API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)para uso.

· O TVSDK não é mais compatível com Capítulos padrão ao usar o Adobe Analytics. Defina e gerencie capítulos usando seu aplicativo.

· A versão contém correções para problemas críticos do cliente. Consulte *Problemas corrigidos *uma lista.

**Versão 2.4.9**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.9 do TVSDK do navegador:

· Fluxos HLS VOD e Live com descontinuidade de tempo, mas sem marcadores de descontinuidade, são compatíveis.

· Quadros ID3 v2.4.0 são compatíveis com a tag de vídeo Safari para VOD HLS e transmissões em tempo real.

· A implementação de carregamento de anúncio seguro garante que as chamadas do servidor de publicidade sejam atualizadas para HTTP seguro com base na configuração da API. Para obter os detalhes, consulte as classes AdobePSDK.AdvertisingMetadata e AdobePSDK.ForceHttpsAdConfiguration. Este recurso não é suportado no modo de fallback do Flash.

· As informações de ID de anúncio e de Extensão associadas às respostas do VAST 3.0 agora são disponibilizadas para o aplicativo pelo TVSDK e podem ser usadas para implementar a integração de Mat para medidas de Anúncios. Para obter os detalhes, consulte a API AdobePSDK.NetworkAdInfo. Isso não é suportado no modo de fallback do Flash.

A classe AdobePSDK.ForceHttpsConfiguration não está mais disponível. É sucedido por

Classe AdobePSDK.ForceHttpsAdConfiguration.

· Uma nova API, AdobePSDK.otimizeFlashCalls, agora está disponível para otimizar as chamadas para melhorar a experiência de reprodução HLS no modo de fallback do Flash. Essa opção está desativada por padrão.

**Novidade na Atualização 2.4.8 (Build 6002)**

Esta atualização contém correções para problemas críticos do cliente. Consulte *Problemas corrigidos*, para a lista.

**Versão 2.4.8**

Os seguintes aprimoramentos e adições estão disponíveis como parte da versão 2.4.8 do TVSDK do navegador:

· O SDK agora é compatível com o Chrome EME e com as alterações de práticas recomendadas disponíveis a partir do Chrome v58. Para obter mais detalhes, consulte [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· A estrutura da interface do usuário agora é compatível com o fluxo de trabalho HLS Access DRM on Flash, Ad only e Targeting Info.

· A API setDRMAuthenticateData é adicionada à Estrutura da interface do usuário. Para reproduzir fluxos protegidos com DRM de Acesso ao Adobe, chame esta API. Como alternativa, o atributo drmAuthenticateData pode ser especificado no reprodutor. Consulte [AdobePSDK.videoBehavior](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)para obter detalhes.

**Versão 2.4.7**

Os seguintes recursos são novos na versão 2.4.7:

· Adição do configurador de interface do usuário na estrutura da interface do usuário

Você pode configurar o reprodutor de uma das seguintes maneiras:

· Uso de um objeto JSON

· Uso de APIs

Para ajudar a gerar o objeto JSON, o TVSDK do navegador fornece uma ferramenta **Configurador de interface do usuário**.

Nesta ferramenta, você pode selecionar várias configurações, clicar em **Testar configuração **para verificar as configurações e clicar em **Baixar configuração**para baixar as configurações. Depois de baixar o arquivo, você pode passar o conteúdo desse arquivo como objeto JSON para a API ptp.videoPlayer.

· Adição da API MediaPlayerItemConfig à Estrutura da interface

Vários recursos, incluindo advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration, podem ser configurados por meio de MediaPlayerItemConfig. Para obter mais informações, consulte a documentação do AdobePSDK.MediaPlayerItemConfig no [API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [documentação](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

Na Estrutura da interface, a maneira de transmitir configurações de rede pela configuração do reprodutor foi modificada.

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

As configurações de DRM e o rastreamento do Analytics podem ser habilitados por meio da Estrutura da interface do usuário.

* Adição de `AdobePSDK.embedSWFinFullScreenDiv` API

Essa nova API oferece flexibilidade ao aplicativo player para selecionar a div na qual ele pode incorporar o arquivo FlashFallback.swf.

* Substituído `getVersion`API de `AdobePSDK.MediaPlayer` classe com `AdobePSDK.Version` classe para informações relacionadas à versão do TVSDK. Para obter detalhes, consulte `AdobePSDK.Version` API [aqui](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versão 2.4.6**

Os seguintes recursos são novos na versão 2.4.6:

* **Suporte a Browserify**

Browserify permite usar os módulos de estilo node.js no navegador. Você pode definir as dependências e o Browserify agrupa tudo em um arquivo JavaScript.

* **Faturamento**

Com a ajuda da cobrança, o TVSDK do navegador pode coletar métricas de uso do player para faturar clientes do Primetime.

>[!NOTE]
>
>O enum MediaPlayer.Events obsoleto e as constantes obsoletas em Enum PSDKErrorCode foram removidos na versão 2.4.6. Para obter mais informações, consulte [Conversão do TVSDK 2.4.5 do navegador para a versão 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versão 2.4.5**

Os seguintes recursos são novos na versão 2.4.5:

* **Repetições completas de evento e anúncios**

  Os fluxos de Repetição de evento completo (FER) do HLS agora oferecem suporte à resolução de anúncios e aos comportamentos de anúncios. Para habilitar esse suporte, defina o modo de sinalização de anúncio como `MANIFEST_CUES` ao criar o `MediaPlayerItemConfig` objeto.

* **Suporte a MediaplayerView ScalePolicy**

  Os desenvolvedores de aplicativos agora podem especificar uma scalePolicy diferente para a exibição usando a propriedade scalePolicy de MediaplayerView.

* **Suporte a conteúdo anamórfico**

  A reprodução de conteúdo anamórfico agora é compatível com o MSE e a reprodução de Flash.

* **Aplicação seletiva de`withCredentials`**

Quando `withCredentials` estiver definido como verdadeiro, a variável `Access-Control-Allow-Origin` o cabeçalho não pode ser definido como curinga. Dependendo da resposta do servidor, o TVSDK do navegador definirá seletivamente as `withCredentials` atributo. Para obter mais informações sobre esse suporte, consulte [Documentos da API TVSDK do navegador](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versão 2.4.4**

Os seguintes recursos eram novos na versão 2.4.4:

* **Aplicativo de amostra do Chromecast**

Esta versão oferece suporte para um aplicativo remetente e destinatário que demonstra a reprodução de fluxos de VOD DASH e fluxos de Widevine DASH com inserção de anúncios do cliente.

* **Suporte avançado a failover**

Esta versão inclui suporte para casos de uso de failover avançado (failover de segmento e servidor) para fluxos de VOD do HLS.

**Versão 2.4.3**

Os seguintes recursos eram novos na versão 2.4.3:

* **Tags personalizadas para DASH VOD**

  Tags personalizadas embutidas (Eventos) podem ser assinadas e recebidas como objeto TimedMetadata.

* **Reprodução de fluxos sem extensões**

  Agora há suporte para fluxos HLS e DASH sem extensões. Para o arquivo de manifesto, o resourceType precisa ser especificado ao carregar o recurso. Para segmentos e arquivos VTT, o cabeçalho de resposta do Tipo de conteúdo é usado para determinar o tipo de conteúdo.

**Versão 2.4.2**

Os seguintes recursos eram novos na versão 2.4.2:

* **Paridade de API**

Para obter uma lista completa da paridade de API, consulte a [Guia de migração do TVSDK para DHLS 1.4 para Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Suporte a AES de exemplo**

  Esta versão adiciona suporte para reprodução de conteúdo criptografado AES de amostra no MSE e fallback do Flash. O requisito de hospedar conteúdo AES em vez de origem segura no Google Chrome foi removido.

* **Suporte para contêineres AAC**

  A reprodução de arquivos com a extensão .aac agora é compatível. Podem ser fluxos somente de áudio ou áudio alternativo.

  >[!NOTE]
  >
  >Os codecs AC3 e AC3 aprimorados ainda não são compatíveis.

* **Reprodução de fluxo com tokens**

Os fluxos HLS entregues por meio de uma Rede de entrega de conteúdo (CDN) às vezes podem usar tokens de autenticação no manifesto e solicitações de segmento para verificação, e esses tokens podem ser fornecidos como parâmetros de URL ou cabeçalhos de cookie. A reprodução desses fluxos agora é compatível.

**Versão 2.4.1**

Os seguintes recursos eram novos na versão 2.4.1:

* **Estrutura da interface**

Essa estrutura, projetada para acelerar o desenvolvimento da interface do usuário para aplicativos de reprodutor de vídeo baseados em JavaScript, consiste em APIs para incluir controles básicos como reprodução/pausa e volume e para adicionar ou remover facilmente elementos, como estados de barra de depuração e configurações de legendas ocultas. Você pode especificar o comportamento associado aos controles, criar controles personalizados e aplicar skin à interface do usuário do player. Tudo isso acontece por meio da estrutura, sem a necessidade de manipular diretamente a estrutura DOM.

* **Aprimoramentos de reprodução de HLS para transmissões em tempo real**

Esta versão suporta descontinuidades causadas pela inserção de anúncios. Ele usa a tag EXT-PROGRAM-DATE-TIME seguida pela tag EXT-MEDIA-SEQUENCE para sincronizar entre perfis de taxa de bits adaptáveis para uma reprodução suave.

* **Suporte para VPAID 2.0**

A definição da interface de veiculação de anúncios do reprodutor de vídeo (VPAID), versão 2.0, fornece uma experiência de mídia avançada para usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo. Esta versão é compatível com anúncios JavaScript VPAID lineares para conteúdo de vídeo sob demanda (VOD).

* **Tags HLS personalizadas**

Os fluxos de mídia podem transportar metadados adicionais na forma de tags no arquivo de lista de reprodução/manifesto. O TVSDK do navegador permite especificar e assinar tags adicionais e ser notificado quando essas tags aparecerem no manifesto.

* **Marcadores de anúncio exibidos na linha do tempo do player**

Esta versão é compatível com a exibição de marcadores de anúncios na linha do tempo do player para conteúdo de VOD e Ao vivo. Você pode ver esse comportamento no reprodutor de referência.

**Compatível com o 2.4**

Os seguintes recursos estavam disponíveis na versão 2.4:

* **Reprodução de áudio MP3**

  Essa versão é compatível com a reprodução de áudio MP3 em navegadores com Media Source Extensions (MSE) e com a tag de vídeo do Safari.

* **Reprodução de vídeo MP4**

  Os seguintes recursos são compatíveis:

   * Reprodução de transmissão única
   * Anúncios MP4 antes e depois da exibição com comportamento e rastreamento de anúncios
   * Anúncios HLS antes e depois da exibição com comportamento e rastreamento de anúncios
   * Anúncios DASH antes e depois da exibição com comportamento e rastreamento de anúncios

## Plataformas compatíveis {#supported-platforms}

O TVSDK do navegador tem requisitos específicos para os níveis de plataformas e software em que ele precisa ser executado. As seguintes plataformas e níveis de software são compatíveis:

### Configurações do desktop {#desktop-configurations}

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

* APPLE OS X

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

* APPLE IOS 9

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
   <td><p><strong>MSE do TVSDK do navegador</strong></p> </td> 
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

Esta é uma lista dos recursos compatíveis e não compatíveis com esta versão:

* *Recursos de áudio MP3 — reprodução principal*
* *Recursos de vídeo MP4 — reprodução principal*
* *Recursos de vídeo MP4 — Ad Insertion principal*

>[!NOTE]
>
>*Nas tabelas de matriz de recursos abaixo, um &quot;Y&quot; significa que o recurso é compatível na versão atual.*

### Recursos de áudio MP3 {#mp-audio-features}

**Tabela 1: Reprodução principal{#table-core-playback}**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD MP3 | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado | Y | Y |

1 A tag de vídeo TVSDK do navegador não é compatível com streaming e DRM. O suporte a codec e container não é o mesmo em todos os navegadores.

2 O padrão do Firefox é o Flash Player versão 41 ou anterior.

### Recursos de áudio MP4 {#mp-audio-features-1}

**Tabela 2: Reprodução principal**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD MP4 | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado | Y | Y |

**Tabela 3: Ad Insertion principal**

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD MP4 | Antes da exibição (MP4) | Não suportado | Y | Y |
| Ad Insertion | VOD MP4 | Pós-rolagem (MP4) | Não suportado | Y | Y |

Para obter mais informações sobre o suporte ao recurso HLS ou DASH, consulte abaixo.

## Matriz de recursos HLS {#hls-feature-matrix}

Esta é a matriz de recursos para os recursos HLS no TVSDK do navegador.

* *Reprodução principal HLS*
* *Recursos avançados de reprodução HLS*
* *Recursos de proteção de conteúdo HLS*
* *Recursos principais de inserção de anúncio do HLS*
* *Recursos avançados de inserção de anúncios do HLS*
* *Integrações HLS*

>[!NOTE]
>
>*Nas tabelas de matriz de recursos abaixo, um &quot;Y&quot; significa que o recurso é compatível na versão atual.*

### Recursos HLS {#hls-features}

Os seguintes recursos são compatíveis:

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
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Reprodução geral (reproduzir, pausar, buscar)</p> </td> 
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
   <td><p>Legendas 608/708</p> </td> 
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
   <td><p>Failover do manifesto</p> </td> 
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
   <td><p>Suporte limitado a QoS</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Suporte para cabeçalhos de cookie</p> </td> 
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
   <td>Áudio de associação tardia</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>redirecionamento 302</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 5: Recursos avançados de reprodução do HLS**

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
   <td><p>Reprodução no deslocamento</p> </td> 
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
   <td><p>Truque Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Truque suave Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Análise de ID3</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Suporte a marcador de descontinuidade</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Fluxos tokenizados</p> </td> 
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

**Tabela 6: Recursos de proteção de conteúdo HLS**

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
   <td><p>Amostra-AES</p> </td> 
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

**Tabela 7: Recursos principais de inserção de anúncios do HLS**

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
   <td><p>Antes da exibição (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Durante a exibição (HLS)</p> </td> 
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
   <td><p>Reempacotamento criativo (MP4 para HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 8: Recursos avançados de inserção de anúncios do HLS**

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
   <td><p>Somente anúncio</p> </td> 
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
   <td><p>Política de publicidade personalizada</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Carregamento de anúncio lento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Não suportado</p> </td> 
   <td><p>Limitação da plataforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anúncios complementares, Anúncios de banner, Anúncios clicáveis</p> </td> 
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

**Tabela 9: Integrações HLS{#table-hls-integrations}**

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
   <td><p>Integração com o Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matriz de recursos do DASH {#dash-feature-matrix}

Esta é a matriz de recursos para os recursos DASH no TVSDK do navegador.

· *Recursos de reprodução principal DASH*

· *DASH Recursos avançados de reprodução*

· *DASH Recursos de proteção de conteúdo*

· *Recursos de inserção de anúncio do DASH Core*

· *DASH Recursos avançados de inserção de anúncios*

· *Integrações DASH*

>[!NOTE]
>
>Nas tabelas de matriz de recursos abaixo, um Y significa que o recurso é compatível na versão atual.

### Recursos do DASH {#dash-features}

Os seguintes recursos são compatíveis:

**Tabela 10: Recursos principais de reprodução do DASH**

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
   <td><p>Reprodução geral (reproduzir, pausar, buscar)</p> </td> 
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
   <td><p>Legendas 608/708</p> </td> 
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
   <td><p>Suporte para cabeçalhos de cookie</p> </td> 
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
   <td><p>Definir controles de taxa de bits adaptáveis</p> </td> 
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
   <td><p>Áudio de associação tardia</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>redirecionamento 302</p> </td> 
   <td><p>Somente VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 11: Recursos de reprodução avançada do DASH**

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
   <td><p>Reprodução no deslocamento</p> </td> 
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
   <td><p>Truque</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Truque suave Play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Reprodução</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Análise de ID3</p> </td> 
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
   <td><p>Fluxos tokenizados</p> </td> 
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

**Tabela 12: DASH Recursos de proteção de conteúdo**

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
   <td><p>Amostra-AES</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Proteção de conteúdo</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Widevine no Chrome, Firefox 47 e posterior e Chromecast</p> <p>· PlayReady no Internet Explorer no Windows 8.1 e Edge</p> <p>· DRM Primetime para Windows Firefox (somente vídeo)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 13: Recursos de inserção de anúncio do DASH Core**

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
   <td><p>Durante a exibição (TRAÇO)</p> </td> 
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
   <td><p>Resolução e comportamentos do anúncio</p> </td> 
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
   <td><p>Reempacotamento criativo (MP4 a DASH)</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 14: Recursos avançados de inserção de anúncios do DASH**

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
   <td><p>Somente anúncio</p> </td> 
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
   <td><p>Política de publicidade personalizada</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Ao vivo</p> </td> 
   <td><p>Carregamento de anúncio lento</p> </td> 
   <td><p>Não suportado</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Anúncios complementares, anúncios em banners, anúncios clicáveis</p> </td> 
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

**Tabela 15: Integrações do DASH**

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
   <td><p>Integração com o Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemas corrigidos {#issues-fixed}

**Problemas corrigidos na atualização 2.4.12 (Build 204)**

Os seguintes problemas foram corrigidos na Atualização do TVSDK do navegador versão 2.4.12 (Build 204):

· **21647**- O TVSDK deve permitir a reprodução automática de vídeo em dispositivos iOS quando o áudio estiver sem áudio.

· **21465**- Erro Acesso de chave do sistema negado é recebido ao reproduzir um fluxo DASH protegido por DRM depois que um fluxo DASH Live é reproduzido.

· **21442**- Ative a reprodução automática de conteúdo na Web do iOS, após a reprodução do anúncio precedente com um gesto do usuário.

· **21240**- API fornecida para filtrar anúncios VPAID analisados de Auditude/VMAP.

**Problemas corrigidos na versão 2.4.11**

Os seguintes problemas foram corrigidos na versão 2.4.11 do TVSDK do navegador:

**Recursos principais de reprodução:**

· **19192**: O TVSDK agora implementa TextFormat:bottomInset e TextFormat:safeArea. Devido a essas melhorias, as legendas ocultas podem ser reposicionadas se a barra de controle for exibida na tela.

· **21009**: as legendas ocultas persistem na tela em caso de busca em descontinuidade até que novas legendas sejam exibidas.

· **21141**: a busca retroativa é rejeitada devido a uma condição de corrida durante a anexação do segmento.

· **21142**: Disponibilizar intervalos de reprodução pesquisáveis quando o reprodutor está no estado INITIALIZED. Devido a essas alterações, a sessão de início na posição agora é suportada.

· **21363**: as legendas ocultas 608/708 estão saindo de sincronia após a inserção de anúncios para fluxos DASH.

**Recursos de inserção de anúncio:**

· **21179**: problemas relacionados ao meio da exibição (pausas longas, quadros pretos) com conteúdo de VOD agora são resolvidos com a configuração correta da propriedade ad.primaryAsset.adParameters.

· **21257**: o arquivo MP4 com a taxa de bits mais alta é selecionado para transcodificação se o MP4 não for um tipo MIME válido e o recurso de reempacotamento criativo estiver habilitado.

· **21361**: O TVSDK agora transmite o sistema de publicidade e a ID de criação da resposta do VAST como parâmetros de consulta na solicitação de empacotamento criativo para oferecer suporte a regras de normalização adicionais.

**Problemas corrigidos na versão 2.4.10**

Os seguintes problemas foram corrigidos na versão 2.4.10 do TVSDK do navegador:

**Recursos principais de reprodução:**

· **21060**: erro de codec inválido lançado com fluxos HLS que contêm descontinuidade e as caixas ISO BMFF são executadas até o fim do fluxo.

· **21045**: a reprodução automática não funciona no iOS após a conclusão da primeira reprodução de vídeo em uma lista de reprodução.

· **20975**: a taxa de quadros é retornada como NaN pelo provedor de QoS no navegador Chrome.

· **20823**: erro de codec sem suporte lançado ao encontrar segmentos sem dados.

· **20769**: o SDK agora começa com a taxa de bits atual na busca, em vez de alternar imediatamente com base na política ABR.

· **20031**: no modo retrato no IE11 (Windows 8.1), a tela de vídeo fica pequena. Recurso de proteção de conteúdo:

· **19316**: ignore segmentos que falham na descriptografia no caso de fluxos HLS AES-128.

**Problemas corrigidos na versão 2.4.9**

Os seguintes problemas foram corrigidos na versão 2.4.9 do TVSDK do navegador:

**Recursos principais de reprodução:**

· **13407**: os fluxos de DASH podem parar se o Firefox interromper o envio do evento &quot;ontimeupdate&quot; durante a reprodução.

· **16380**: durante a reprodução de conteúdo de áudio misto de segmentos com tempos de início não correspondentes via MSE, o erro de sincronização de áudio entre representações é acumulado em switches ABR, resultando em erro (problema Chromium #663686).

· **17985**: ao reproduzir um fluxo ISO-BMFF específico no navegador Firefox, a reprodução fica paralisada (Firefox issue #1342913). Isso foi corrigido desde o Firefox v53.

· **19141**: ReferenceError não capturado (na promessa): a largura não está definida.

· **18997, 19299**: problema de cintilação do vídeo no limite do segmento. Isso acontecia porque o SDK não calculava corretamente o deslocamento de tempo de Composição da última amostra.

· **19780**: a reprodução não é iniciada para o conteúdo HLS e HLS Ad no Firefox v53 (Firefox issue #354653).

· **20046**: a Data e hora do programa é recebida como chave em vez de valor quando recebida como objeto de metadados cronometrado.

· **20047**: useDefaultResizeHandler gera um erro com fallback de Flash.

· **20179**: o fallback do Flash não funciona com o Flash Player v25.0.0.171.

· **20293**: o Firefox interrompe o buffering de dados para determinados fluxos HLS, levando a paralisação.

· **20626**: o Player lança um erro de decodificação de mídia no Chrome devido ao manuseio incorreto de amostras de vídeo com duração zero.

· **20078**: a reprodução é interrompida no erro do navegador &quot;QuotaExceeded&quot;.

· **18639**: no HLS Live stream 608 CC, o texto às vezes aparece como incorreto.

· **20028**: o parâmetro de tamanho ClosedCaptions não altera o tamanho da fonte.

· **20613**: as caixas de legendas ocultas se sobrepõem, tornando-as ilegíveis.

**Recursos do Ad Insertion principal (CSAI):**

· **20043**: impressão de anúncio ausente e chamadas de rastreamento de anúncio com vários anúncios e redirecionamentos de terceiros.

· **2004**: ao usar o reempacotamento criativo, todos os anúncios no ad break precisam ser reempacotados com êxito, caso contrário, o ad break é completamente descartado.

· **20097**: a reprodução do anúncio é ignorada e o conteúdo principal é retomado imediatamente, em vez de aguardar o tempo limite de 20 segundos se o manifesto do anúncio não estiver disponível.

**Problemas corrigidos na atualização da versão 2.4.8 (Build 6002)**

Os seguintes problemas foram corrigidos na Atualização do TVSDK do navegador versão 2.4.8 (Build 6002):

· **14126:** A reprodução pode parar no Firefox (issue #1316024) devido a uma lacuna interna no buffer de origem do MSE. Tente buscar para retomar a reprodução

· **19608** Correção para honrar o valor de timeoffset da resposta VMAP Auditude.

· **19635:** Corrige a paralisação de vídeo no Internet Explorer 11 no Windows 10.

· **19761:** Correções para problemas de ABR com HLS.

· **19780** Corrige a reprodução de anúncio com conteúdo HLS corrompido no Mozilla Firefox v53.

· **1987 e 1974:** Os problemas corrigem a inconsistência na seleção da taxa de bits após uma operação de busca. Agora, a seleção da taxa de bits na busca é o valor mais baixo da taxa de bits atual e da taxa de bits na inicialização.

· **19881** A reprodução travada e a sobreposição de buffering são exibidas por tempo infinito depois que a busca é executada de 3 a 4 vezes.

· **19884** Confirme a conformidade com os requisitos de Caminho de mídia verificado (VMP) do Chrome 59 Beta. O bTVSDK conseguiu reproduzir o conteúdo DRM Widevine com o Chrome 59 Beta.

· **19916** A reprodução de DRM na Estrutura da Interface do Usuário foi interrompida. Agora, ele invoca o acquisitionLicense mesmo se não houver política nos metadados.

**Problemas corrigidos na versão 2.4.8**

Os seguintes problemas foram corrigidos na versão 2.4.8 do TVSDK do navegador:

· **10075**: quando a busca antes da linha do tempo, o evento de reprodução concluída não foi recebido no Firefox e no Chrome e o evento de busca não foi recebido no Firefox.

· **15775**: evento de reprodução concluída não recebido no Windows 8.1 Internet Explorer.

· **17306**: para fluxos SAI, a reprodução é compatível. O rastreamento do anúncio compilado não é suportado.

· **19142**: às vezes, o retrocesso faz com que o reprodutor de vídeo permaneça no estado de buffer para sempre.

· **19218**: os marcadores de anúncio não estão disponíveis na estrutura da interface do usuário.

· **19219**: A reprodução de anúncios somente não funciona pela estrutura da interface do usuário.

· **19222**: a chave AES-128 é solicitada uma vez para uma lista de reprodução e as solicitações subsequentes são enviadas do cache. Anteriormente, era solicitado para cada segmento.

· **19597**: &quot;Uncaught TypeError: Não é possível ler a propriedade &#39;log&#39; de indefinido&quot; foi visto com builds canárias do Chrome.

· **19605**: adRequestDomain não estava disponível no modo Fallback de Flash.

· **19608**: os anúncios VMAP não eram inseridos para fluxos HLS Live. O SDK agora considera os marcadores de sinalização e não depende dos valores de deslocamento de tempo nas respostas do VMAP.

· **19637**: a reprodução de anúncios somente leva a um erro de script no final do anúncio.

· **19732**: as solicitações de lista de reprodução CRS falhavam com o erro 404. As solicitações 1401 e 1403 do TVSDK do navegador foram atualizadas para resolver isso.

· **19762**: acquisitionLicense costumava ser chamado antes de setAuthenticationToken, pois uma licença válida foi retornada independentemente da validade do token. Isso foi corrigido agora e acquisitionLicense é chamado somente após a resposta setAuthenticationToken.

**Problemas corrigidos na versão 2.4.7**

Os seguintes problemas foram corrigidos na versão 2.4.7:

· **8397**: os fluxos HLS Live gerados pelo Adobe Media Server podem não ser reproduzidos se os segmentos não começarem com um quadro Principal.

· **13606**: vários problemas relacionados à Busca foram corrigidos para o fluxo HLS no navegador Chrome.

· **14807**: No navegador Chrome, se a busca ou pausa for acionada imediatamente após play(), a reprodução pode parar com o erro DOMException: a solicitação play() foi interrompida por uma chamada... (problema Chromium# 593273).

· **19085**: Parâmetros do MediaPlayer, como volume, abrControlParameters e ccStyle, não são definidos como Padrões ao redefinir o player.

**Problemas corrigidos na versão 2.4.6**

O seguinte problema foi corrigido na versão 2.4.6:

· **18093**: TimedMetadata para a tag ao lado da tag inscrita é retornado quando você usa a versão 24 do Flash Player no modo Fallback de Flash.

**Problemas corrigidos na versão 2.4.4**

Os seguintes problemas foram corrigidos na versão 2.4.4:

· **8711**: no MSE, as legendas 608/708 são deixadas justificadas por padrão.

· **13934**: as configurações ABR para anúncios não são aplicáveis ao reproduzir com transmissões HLS Live.

· **14079**: a longevidade para fluxos ao vivo HLS com janela DVR baixa pode falhar, pois a reprodução pode ficar para trás devido a problemas de latência de rede. Clique no ponto ativo para retomar a reprodução.

· **15037**: as amostras fornecidas com a estrutura da interface do usuário do player não funcionam no Microsoft Internet Explorer 10 no Windows 7.

· **15913**: para fluxos de VOD HLS, no Chrome, o fluxo não será reproduzido se a resposta do manifesto for 304 não modificada. Isso foi corrigido desde o Chrome v55 (problema de Chromium 633696).

· **16103**: No Android Chrome, em condições de baixa largura de banda, a reprodução pode parar com o TypeError não capturado: não é possível ler a propriedade &#39;programDateTime&#39; de erro indefinido.

· **16265**: para VOD HLS e transmissões em tempo real, a busca entre descontinuidades não funciona.

· **16709**: Retomar o fluxo do HLS Live com PDT e marcador de descontinuidade pode fazer com que o player fique preso no buffering.

## Problemas conhecidos e limitações {#known-issues-and-limitations}

As limitações e problemas conhecidos no TVSDK do navegador são mencionados abaixo.

**Tabela 16: Recursos principais de reprodução**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (somente reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Reprodução geral (Reproduzir, Pausar, Buscar)</td> 
   <td><p>· Formatos de mídia diferentes de HLS não são compatíveis.</p> <p>8799: o fallback do Flash não cuida do conteúdo misto e, portanto, é necessário garantir que o Conteúdo, o Anúncio e outros URLs não resultem em conteúdo misto (conteúdo seguro e não seguro juntos).</p> <p>19271: a reprodução de várias visualizações por meio da estrutura da interface do usuário não é compatível no modo de fallback do Flash.</p> <p>· O fallback do Flash não funciona no Microsoft Internet Explorer 8 e 9 no Windows 7, pois essas versões não são compatíveis com o SDK.</p> <p>20262: o fallback do Flash adiciona parâmetros personalizados à lista de informações de direcionamento. Além disso, a ordem de prioridade dos parâmetros personalizados é diferente no caso do Flash e do MSE.</p> <p>20653:o fallback do Flash TVSDK do navegador não funciona no Win10 com a Atualização de Criadores.</p> <p>· O Flash Fallback funciona com o Flash Player versão 23 e posterior.</p> <p>· 20087 - Chrome 59 Beta com</p> <p>Flash 25.0.0.171</p> <p>Beta (padrão), a reprodução HLS não está funcionando no modo Fallback do Flash. Está funcionando bem em Canárias.</p> </td> 
   <td><p>12563: Fluxos de traço com codec de áudio mp4a.40.02 não são reproduzidos no Firefox devido a uma sequência de codec de áudio não compatível no MPD. O Codec de áudio mp4a.40.2 é compatível.</p> <p>15029: Ao alternar entre vídeos no multiView na UI-Framework, o botão reproduzir/pausar não é atualizado adequadamente.</p> <p>16034:No Windows 8.1 IE, chamar reset() leva ao erro de tipo Desconhecido MIME. Recarregue a mídia para retomar a reprodução.</p> <p>18235: Certos problemas de busca são observados com fluxos de Vod DASH com anúncios.</p> <p>18727: API de erro não compatível com o MSE</p> <p>18750: Os eventos de Alteração de Status podem estar fora de ordem em alguns casos para a estrutura do SDK e da interface do usuário e na Estrutura da interface do usuário, os eventos IDLE e Initializing StatusChange podem estar ausentes para os Ouvintes de eventos adicionados após o carregamento do recurso.</p> <p>18889: Se o MediaPlayer estiver no estado ERROR, o objeto de exibição não será retornado.</p> <p>· 19039: Se AdobePSDK. MediaPlayer. seekToLocal() é usado com um valor maior que EOF e, em seguida, a reprodução começa a partir do início, no caso de MSE.</p> <p>19049: Nenhum estado de erro relatado para o Flash Player no Chrome, IE, Firefox quando o vídeo é bloqueado durante a reprodução.</p> <p>17205: A reprodução de vídeo é interrompida ao reproduzir fluxo não muxado por algumas horas enquanto o áudio continua a ser reproduzido (Chromium edição nº 664033).</p> <p>12308: os fluxos DASH com composition_ time_offset especificados podem ter timeStampOffset aplicado a eles no navegador Chrome, resultando em um tempo de decodificação negativo e, portanto, em MEDIA_ERR_ SRC_NOT_ SUPPORTED error (Chromium issue #398141).</p> <p>14126: A reprodução pode parar no Firefox (problema nº 1316024) devido a uma lacuna interna no buffer de origem do MSE. Tente buscar para retomar a reprodução.</p> <p>19115: MS Edge e IE 11 (Win 8.1 e 10) não definem Origin como nulo no redirecionamento CORS e ainda falham porque o cabeçalho não é nulo, resultando em erro de reprodução.</p> <p>· 19861:Problema com o comportamento de acréscimo no buffer de origem para mídia já reproduzida. O Chrome rejeita o fragmento anexado, incluindo o moov, causando erro de decodificação subsequente. (Chromium issue #735335)</p> <p>19921: a reprodução é interrompida para determinado conteúdo HLS, mesmo que ele seja armazenado em buffer com sucesso (Chromium issue #713540)</p> <p>20444:buscar o fim do intervalo em buffer no IE e no Edge pode causar paralisação da reprodução.</p> <p>20511: às vezes, a rejeição de busca pode ser observada para fluxos HLS com ou sem anúncios.</p> <p>· 20743: No Windows 10 Chrome, o fluxo do HLS Live é reproduzido por alguns segundos antes da reprodução de pré-implantação do MP4.</p> <p>21043: A dimensão do vídeo pode não estar correta no carregamento inicial devido à falta de metadados.</p> <p>· 21115: O gesto do usuário do Android é necessário para iniciar a reprodução se o anúncio precedente estiver disponível para vídeos em uma lista de reprodução.</p> <p>· O HLS Live não oferece suporte à sobreposição de carimbo de data/hora.</p> <p>· O áudio AAC-SSR não é compatível.</p> <p>Os codecs de áudio AC3 e Enhanced AC3 não são suportados.</p> <p>· Para fluxos com descontinuidade de carimbo de data e hora, mas sem marcadores de descontinuidade</p> <p>· A reprodução pode ter falhas e busca incorreta devido a saltos.</p> <p>· A duração do conteúdo e a duração da reprodução podem não ser iguais.</p> <p>· As descontinuidades entre representações e representações devem corresponder a outros fatores, o que pode levar a problemas de sincronização e paralisação.</p> <p>· As legendas e a WebVTT podem não aparecer perto do fim do fluxo.</p> <p>· As alterações no codec de áudio não são suportadas em saltos de carimbo de data e hora.</p> <p>· A inserção de anúncios não é suportada.</p> <p>· O modo de truque rápido pode levar ao loop de reprodução no Win 8.1 IE 11 (MS issue #12446268).</p> <p>TRAÇO:</p> <p>· Para transmissões ao vivo - o perfil ao vivo com tipo dinâmico é compatível.</p> <p>· Para fluxos VoD — o perfil ativo com tipo estático é compatível.</p> <p>Para fluxos de VoD - o perfil sob demanda não é certificado para fluxos de trabalho de anúncio.</p> </td> 
   <td><p>· Os fluxos DASH Live e DASH Video on Demand não são compatíveis.</p> <p>· A reprodução de vídeo PIP (Picture in Picture) não é compatível com o iOS no modo de tela cheia.</p> <p>No Safari (tag de vídeo), a extensão sem manifesto sem ter o cabeçalho de tipo de conteúdo correto não funciona.</p> </td> 
   <td><p>· A applicationID no aplicativo do remetente precisa ser a mesma gerada no registro do URL do Destinatário como um aplicativo Destinatário personalizado.</p> <p>· O reprodutor de referência é certificado para workflows DASH. A estrutura da interface do usuário não está certificada.</p> <p>Para obter a lista de codecs de mídia compatíveis, consulte <a href="https://developers.google.com/cast/docs/media"><em>aqui</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Reprodução geral (Reproduzir, Pausar, Buscar)</td> 
   <td> </td> 
   <td>18098: Certos problemas de busca são observados com o fluxo FER do LBA HLS.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Taxa de bits adaptável</td> 
   <td><p>20079: regravação de buffer na busca dentro do intervalo de buffer.</p> <p>20080: o comportamento ABR do Flash está em inconsistência com o MSE.</p> </td> 
   <td><p>· A variante de fallback somente de áudio em um fluxo ABR é ignorada devido às limitações relacionadas a buffer.</p> <p>12289: os parâmetros de controle ABR não se aplicam ao áudio no caso de fluxos HLS/DASH não muxados.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Legendas 608/708</td> 
   <td> </td> 
   <td><p>7810: No Android 4.4.4, o Chrome não parece ter suporte para famílias de fontes CSS básicas usadas pelo reprodutor e, portanto, a função de alteração de estilo de fonte não está funcionando.</p> <p>· Os canais CC não podem ser alterados no caso de legendas 608.</p> <p>· Os recursos de estilo avançados não são compatíveis com as legendas 608.</p> <p>São suportadas as Legendas incorporadas (608/708), sinalizadas via tag de acessibilidade.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>5206: as tags de região no arquivo WebVTT são ignoradas pelo reprodutor ao exibir as legendas.</p> <p>· DASH: Arquivos VTT fragmentados/segmentados não são compatíveis.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Failover de manifesto</td> 
   <td>21056: Com o Flash Fallback, o failover não ocorre para o fluxo ao vivo se o fluxo principal retornar um erro 404 durante a reprodução.</td> 
   <td>O failover de manifesto é aplicável apenas para conteúdo, não para anúncios.</td> 
   <td>O failover da lista de reprodução ausente funciona no Safari somente para o código de erro HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Failover avançado</td> 
   <td> </td> 
   <td><p>· O failover de segmento não permite ignorar segmentos indisponíveis e continuar a reprodução.</p> <p>20533: os segmentos ausentes em uma lista de reprodução devem ser tratados como uma Descontinuidade e a reprodução deve retomar do próximo segmento disponível.</p> <p>21267: a alternância de fluxo devido a failover pode levar ao download de segmentos mais antigos.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Notificações de QoS e Player</td> 
   <td>21129: a taxa de quadros não está disponível no caso de Fallback de Flash.</td> 
   <td><p>• 11170:</p> <p>Timed_Event não está disponível para TVSDK de navegador com MSE, ao contrário de TVSDK de navegador com fallback de Flash.</p> <p>21129: a taxa de quadros não é calculada para fluxos ao vivo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Suporte para cabeçalhos de cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>O sinalizador withCredentials e os cabeçalhos de cookie não são compatíveis com o Safari.</p> <p>21051: Para permitir cookies no Safari, habilite a configuração "Cookies e dados do site" em Preferências &gt; Privacidade.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Tags personalizadas</td> 
   <td>14763: Tags personalizadas diferentes de iniciar com # não devem ser suportadas. No momento, o objeto TimedMetadata é criado e relatado para essas tags durante o Fallback de Flash.</td> 
   <td>Fluxos com tags personalizadas em banda não são certificados.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Áudio de ligação tardia</td> 
   <td> </td> 
   <td><p>· A inserção de anúncios não é compatível com fluxos HLS Live LBA.</p> <p>· 17273: Os fluxos de LBA HLS VOD alternam para representação padrão em caso de failover e não podem ser alternados de volta para a última seleção.</p> <p>· 20251: O fluxo do LBA do HLS Live pode parar na busca.</p> <p>· 20497: O player permanece no estado de buffering se os fluxos não muxados do LBA do HLS tiverem quadros de áudio ou vídeo ausentes perto do fim do fluxo.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Redirecionamento 302</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>não há suporte para otimização de redirecionamento nos navegadores Windows Edge e IE, pois eles não oferecem suporte à propriedade responseURL no objeto XMLHttpRequest.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 17: Recursos avançados de reprodução**

<table> 
 <tbody> 
  <tr> 
   <td>Tipo de conteúdo</td> 
   <td>Recurso</td> 
   <td>Flash</td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (somente reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Reprodução no deslocamento</td> 
   <td><p>Não há suporte para iniciar a reprodução em um valor de deslocamento específico para o conteúdo MP4.</p> </td> 
   <td>20492: Os anúncios intermediários antes do deslocamento são reproduzidos antes que o conteúdo seja retomado do valor do deslocamento.</td> 
   <td>A reprodução com o recurso de deslocamento não é compatível com o iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Truque Play</td> 
   <td>O Smooth Trickplay não funciona para fluxos sem representações de iFrame.</td> 
   <td><p>· As adaptações de Truque Reproduzir não são suportadas no Firefox e no Internet Explorer e, portanto, o modo de truque reverso não está disponível nesses navegadores.</p> <p>· O Truckplay não está disponível ao reproduzir conteúdo junto com anúncios.</p> <p>10435: Durante a reprodução DASH, o vídeo congela no forward trick play no Internet Explorer (Win 8.1)</p> <p>intermitentemente. Isso está acontecendo, pois estamos usando a propriedade playbackRate de elementos de vídeo sem a adaptação de truque de reprodução.</p> <p>14182: Às vezes, durante o retrocesso no navegador Chrome, o evento de busca pode não ser recebido e, portanto, o modo de truque não funcionará.</p> <p>· 14942: As taxas de reprodução podem ser definidas no Chrome para Android mesmo no caso de fluxos de reprodução não enganosos, mas a configuração não será aplicada e a reprodução continuará na taxa normal.</p> <p>17308: Seek não funciona no modo Trickplay.</p> <p>17309: No navegador Chrome, o modo de truque reverso não pode ser mantido por mais de 2 segundos.</p> <p>19272: A reprodução de truques pode não se recuperar do buffering no navegador Windows 10 Edge no caso de fluxos DASH.</p> </td> 
   <td>O modo de truque de retrocesso não é compatível.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Análise de ID3</td> 
   <td>20346: O byte de codificação de texto de quadros ID3 também deve ser retornado pelo SDK.</td> 
   <td><p>As tags ID3 disponíveis em fluxos de transporte de dados de áudio (ADTS) são ignoradas pelo SDK.</p> <p>12378: Os metadados cronometrados da ID3 são analisados em momentos diferentes no Flash e no navegador com suporte ao MSE e, portanto, o comportamento de exibição na linha do tempo do reprodutor de referência também é diferente.</p> <p>19247: a análise de ID3 não é compatível com a estrutura da interface do usuário.</p> </td> 
   <td><p>20323: a tag PRIV ID3 usada para sinalizar o carimbo de data e hora da primeira amostra de segmento aac não é analisada pelo Safari (Safari issue #32422733)</p> <p>20350: em determinados dispositivos (incluindo MAC OS X 10.1, iPad10), o Safari não fornece o evento de alteração de sinalização quando em modo de truque e, portanto, quadros ID3 não são recebidos. (Safari issue #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Suporte a marcador de descontinuidade</td> 
   <td> </td> 
   <td><p>· A inserção de anúncios no lado do cliente não é compatível com fluxos HLS que contenham descontinuidade.</p> <p>· A alteração do Codec de áudio não é permitida em descontinuidades no fluxo HLS.</p> <p>· O switch de rastreamento de áudio não é compatível com o fluxo HLS com marcadores de descontinuidade</p> </td> 
   <td>O número de sequência de descontinuidade é um requisito para fluxos HLS com descontinuidade, a fim de reproduzir no Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 18: Recursos de proteção de conteúdo**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (somente reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>O intervalo de bytes não é compatível com o conteúdo criptografado AES-128.</td> 
   <td>12324: Fluxos criptografados AES-128 do HLS falham na reprodução no Safari se a tag IV não for especificada.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>12660: HTML5 player lança Internal Server Error para conteúdos expirados do traço criptografado PlayReady.</p> <p>· 16720: o conteúdo criptografado DASH DRM não funcionará se o atributo de início na tag period estiver ausente.</p> <p>· 18589: A reprodução não é compatível com DRM protegido Dash VoD Multiperiod streams com Xlink.</p> <p>18653: A reprodução de conteúdo Widevine MultiPeriod com Várias Chaves é interrompida no primeiro período e não pode mudar para o próximo Período.</p> <p>18656: Fluxo MultiPeriod Playready, criptografado com chaves diferentes, não é reproduzido.</p> <p>O Playready 2.0 para Dash não é certificado.</p> <p> </p> <p> </p> </td> 
   <td>12602: Os metadados de DRM HLS Fairplay são atualizados repetidamente pelo reprodutor HTML5 no Safari</td> 
   <td><p>DASH Widevine DRM conteúdo embalado através Bento4 pode ser reproduzido. O conteúdo empacotado por meio do Offline Packager e do Shaka Packager não é reproduzido. DASH PlayReady DRM não é compatível.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 19: Recursos do Ad Insertion principal (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (somente reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Pré/Meio/Pós</td> 
   <td> </td> 
   <td><p>· Anúncios anteriores com conteúdo HLS ao vivo são reproduzidos no modo Dual player.</p> <p>· Anúncios DASH com conteúdo HLS e anúncios HLS com conteúdo DASH não são suportados.</p> <p>19002: No HTML5 Player com MSE adBreak. insertionType não retorna o valor correto para descrever o tipo de inserção correto, ou seja, cliente inserido e/ou servidor inserido.</p> <p>7794: Em dispositivos móveis (iOS, Android com Chrome 33 ou inferior ou Navegador nativo) onde a barra de controle padrão está visível no modo de tela cheia, a barra de busca e os botões de avanço rápido estão disponíveis quando os anúncios são reproduzidos.</p> <p>· 11048: Alternar do anúncio para o conteúdo HLS Live não é tranquilo no caso de extensões de origem de mídia.</p> <p>16083: No Android 4.4 Chrome v52, às vezes, o anúncio HLS com conteúdo HLS pode levar a um erro de decodificação de pipeline após uma reprodução interrompida.</p> <p>16097: Erros encontrados durante o Ad break não são tratados, pode fazer com que o fluxo principal interrompa a reprodução.</p> <p>· 18095: Os anúncios MP4 não são compatíveis com o conteúdo HLS live.</p> <p>19120: várias buscas em anúncios HLS com conteúdo HLS podem fazer com que o fluxo interrompa a reprodução.</p> <p>· 19131: A sobreposição de buffering pode aparecer ao alternar do ad break precedente para o conteúdo.</p> <p>· 20296: No caso de transmissões ao vivo HLS, buscar de volta na janela DVR seguido por buscar sobre rolls médios resolvidos pode levar à paralisação da reprodução.</p> <p>· 20298:Fluxos HLS Live com rolos médios param o momento em que o primeiro anúncio intermediário sai da janela do DVR.</p> <p>· 20317: Os fluxos HLS Live podem parar ao alternar para o próximo anúncio ou de anúncio para conteúdo caso o ad break contenha mais de um anúncio.</p> 
    <ul> 
     <li>Os anúncios na janela DVR de transmissões HLS Live não são resolvidos.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>O SDK não respeita o atributo de sequência na resposta do VMAP para o VAST AdSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: o SDK não respeita o atributo de sequência dentro da resposta do VMAP para o VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: Não há suporte para atributo de repetição VMAP.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Reempacotamento criativo</td> 
   <td> </td> 
   <td>21464: A resposta do anúncio é completamente descartada se o reempacotamento criativo falhar para um dos anúncios no ad break.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 20: Recursos avançados do Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo de conteúdo</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 no Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 no Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (somente reprodução DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Somente anúncio</td> 
   <td> </td> 
   <td>20056: A propriedade da tecnologia do player não é relevante, pois é baseada no conteúdo principal que está vazio no caso de reprodução Somente de anúncio</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Ao vivo</td> 
   <td>Política de publicidade personalizada</td> 
   <td> </td> 
   <td><p>· Comportamentos de anúncios não são compatíveis com anúncios MP4 e conteúdo MP4.</p> <p>13973: Comportamentos de anúncios personalizados - a política IGNORAR não gera um evento concluído quando usada com o MSE.</p> <p>14939: as políticas de comportamento de anúncio personalizadas ignoram e ignoram a quebra de anúncio não funcionam para o conteúdo DASH.</p> <p>17131: O primeiro quadro do anúncio fica visível e o conteúdo é retomado no caso de IGNORAR a política de ad break.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Anúncios de companhia/anúncios em banner/anúncios clicáveis</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Os anúncios de banner não estão visíveis ao usar o reprodutor de referência.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· Comportamentos de anúncios não são compatíveis com anúncios VPAID.</p> <p>15032: Anúncios VPAID em combinação com anúncios MP4 ou HLS em um ad break não são compatíveis.</p> <p>19001: No Android e iOS, quando um anúncio VPAID é reproduzido com MP4, como conteúdo principal, as faixas de áudio duplas são audíveis, uma de conteúdo principal e outra de anúncio.</p> <p>· 20762: Anúncios VPAID não são compatíveis com o Picture in Picture (PIP).</p> <p>21172: O evento Play complete não é recebido para conteúdo HLS VOD com anúncios VPAID.</p> <p>21173: onAdBreakCompleteEvent não é recebido para conteúdo de VOD do HLS e anúncios VPAID pós-lançamento.</p> </td> 
   <td>O player alterna entre o modo normal e o modo de tela cheia ao alternar entre o anúncio VPAID e o conteúdo principal.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabela 21: Integrações**

| **Tipo de conteúdo** | **Recurso** | **Flash** | **HTML5 no Firefox, IE, Chrome, Android Chrome** | **HTML5 no Safari, iOS Safari** | **Chromecast (somente reprodução DASH)** |
|---|---|---|---|---|---|
| VOD + Ao vivo | Integração com o Adobe Analytics VHL |  | 19004: O rastreamento do Video Analytics não está disponível por meio da Ferramenta de configuração da interface do usuário. |  |  |

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) página.
