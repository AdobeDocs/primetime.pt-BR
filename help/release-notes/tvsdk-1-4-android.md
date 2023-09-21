---
title: Notas de versão do TVSDK 1.4 para Android
description: As Notas de versão do TVSDK 1.4 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# Notas de versão do TVSDK 1.4 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 1.4 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas de dispositivo no TVSDK Android 1.4.

## Novos recursos {#new-features}

**Versão 1.4.43**

**Carregamento de anúncio seguro em HTTPS**

O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios primetime e CRS em HTTPS.

**alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando esse parâmetro for definido, use a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

Ele aceita um valor de parâmetros booleanos. Se o valor for `True`, o cliente usa a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

**Versão 1.4.42**

**Inserção parcial de ad-break:**
Experiência semelhante à de TV ao ingressar no meio de um anúncio sem disparar o rastreamento do anúncio parcialmente assistido.
Exemplo: o usuário se junta ao meio (a 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. São 10 segundos do segundo anúncio no intervalo.
* O segundo anúncio é reproduzido pelo tempo restante (20 segundos) seguido pelo terceiro anúncio.
* Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente para o terceiro anúncio são acionados.

**Versão 1.4.41**

Sem novos recursos.

**Versão 1.4.40**

Sem novos recursos.

>[!NOTE]
>
>Você não exigirá as alterações na API se estiver em uma versão anterior à 1.4.39.

**Versão 1.4.39**

* O TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.
* O Android TVSDK foi atualizado para fazer solicitações do CRS do novo host do Akamai `primetime-a.akamaihd.net`.
* A nova configuração do nome de host fornece a entrega de ativos CRS por HTTP e HTTPS (SSL) em maior escala.
* O TVSDK é compatível com a versão Android Oreo.
* Uma nova função é adicionada a `AdClientFactory` classe para dar suporte ao registro de vários Detectores de Oportunidades:

  ```
  public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
  ```

  Isso deve retornar uma matriz de PlacementOpportunityDetector. Agora você pode registrar vários Detectores de oportunidade. Por exemplo, para o recurso de saída antecipada de anúncios, dois Detectores de oportunidade eram necessários: um para inserção de anúncios e outro para saída antecipada de anúncios. É necessário implementar essa nova função para afetar somente se você tiver implementado seu próprio AdvertisingFactory (e não usar DefaultAdvertisingfactory). Para obter o comportamento existente, é necessário criar um único Detector de oportunidades, como na função createOpportunityDetector(), colocá-lo em uma matriz e retornar:

  ```
  public class MyAdvertisingFactory extends AdvertisingFactory {  
  …  
  @Override  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
  return opportunityDetectors;  
  } }
  ```

>[!NOTE]
>
>Você não exigirá as alterações na API se estiver em uma versão anterior à 1.4.39.

**Versão 1.4.36**

Correção de erros para Ignorar conteúdo no Android.

**Versão 1.4.35**

* **Informações sobre Anúncios de Rede**

  As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. A ID do anúncio, o Sistema de publicidade e as Extensões de anúncios VAST são fornecidos na classe NetworkAdInfo acessível por meio da propriedade networkAdInfo em um Ativo de publicidade. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como **Análise do Mat**.

**Versão 1.4.31**

**Suporte a várias CDNs para anúncios CRS**
* Por padrão, todos os ativos transcodificados serão hospedados no CDN de propriedade do Adobe no Akamai. Com a versão mais recente, o Adobe Creative Repackaging Service (CRS) fornece a capacidade de fazer upload dos dispositivos de criação transcodificados para vários CDNs, conforme especificado pelo cliente.
* Novas APIs são adicionadas ao TVSDK para permitir a especificação do URL criativo final do CRS quando o URL padrão não for usado. Consulte a documentação para saber como usar essas novas APIs.

**Versão 1.4.18**
O Primetime Android TVSDK agora é compatível com criações JavaScript VPAID 2.0 para permitir uma experiência avançada de anúncios interativos em fluxo. Para obter mais informações sobre o VPAID 2.0, consulte [Suporte a anúncios VPAID](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versão 1.4.17**

O AC-3 5.1 é compatível somente com o Amazon FireTV.

**Versão 1.4.11**

* **Fallback de anúncios, encadeamento de Daisy na lógica de seleção de anúncios (Zendesk #3103** Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Fallback de anúncios para anúncios VAST e VMAP](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Biblioteca de Video Heartbeats (VHL) atualizada para a versão 1.5**
   * Capacidade de enviar metadados com início de vídeo e/ou início de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - As pulsações são menores em média e menores em tamanho

**Versão 1.4.7**

* **Suporte à individualização no local** Suporte para instalações locais do Adobe Individualization Server para personalizar a solicitação de individualização do cliente para ir para um endpoint diferente.

**Versão 1.4.6**

* **Criptografia AES de amostra (requer o Flash Player versão 17.0.0.134)**A criptografia AES baseada em amostra agora é compatível.

**Versão 1.4.2**

* **Atualização da Biblioteca de vídeo Heartbeats (VHL) para a versão 1.4.0.1**

   * Adição da capacidade de reunir diferentes casos de uso de análise, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete. O ad break é inferido das chamadas de método trackAdStart e trackAdComplete.
   * A propriedade de indicador de reprodução não é mais necessária ao rastrear anúncios.

* **Integração do SDK Nielsen** O TVSDK agora oferece suporte ao envio de informações de rastreamento do usuário para o SDK Nielsen sem qualquer integração personalizada.

**Versão 1.4.0**

* **Sinalização De Blecaute Com Substituição De Conteúdo Alternativo** Como parte da atualização do TVSDK 1.4, o TVSDK também oferece suporte à entrada e ao retorno de blecautes regionais em relação ao conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando a programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remova/substitua anúncios C3** Agora, nenhum trabalho preparatório adicional é necessário para inserir dinamicamente novos anúncios nos ativos de vídeo sob demanda (VOD) que saem da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova e poderosa funcionalidade também é útil nos casos em que o conteúdo ao vivo/linear é transmitido e é imediatamente desativado para uso como conteúdo sob demanda sem o tempo adequado para &quot;limpar&quot; o ativo.

* A interface PlaybackEventListener tem um novo método chamado onReplaceMediaPlayerItem, que você pode usar para acompanhar um novo evento, `ITEM_REPLACED`. Esse evento é despachado sempre que uma ocorrência de MediaPlayerItem é substituída no MediaPlayer. O aplicativo cliente que implementa este PlaybackEventListener deve implementar ou substituir este novo método.
* AdClientFactory tem uma nova função adicionada à classe para registrar vários Detectores de Oportunidade:

  ```
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
  
  For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
  
  To override this new function create a single Opportunity Detector, and put into an array and return:
  
  @Override
  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
  
  return opportunityDetectors;
  }
  
  }
  ```

## Alterações de TVSDK para 1.4 {#tvsdk-changes}

* A interface PlaybackEventListener tem um novo método chamado onReplaceMediaPlayerItem, que você pode usar para acompanhar um novo evento, ITEM_REPLACED. Esse evento é despachado sempre que uma ocorrência de MediaPlayerItem é substituída no MediaPlayer. O aplicativo cliente que implementa este PlaybackEventListener deve implementar ou substituir este novo método.

* AdClientFactory tem uma nova função adicionada à classe para registrar vários Detectores de Oportunidade:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Por exemplo, para o recurso de saída antecipada de anúncios, você precisa de dois Detectores de oportunidade - um para inserção de anúncios e outro para saída antecipada de anúncios.

Para substituir essa nova função, crie um único Detector de oportunidades, coloque em um storage e retorne:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Certificação e suporte a dispositivos na versão 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Os seguintes recursos são **não** compatível com o TVSDK:
>
>* Câmera lenta, em qualquer plataforma ou versão.
>* Jogo ao vivo.

**Versão 1.4.43**

O TVSDK 1.4.43 foi certificado com dispositivos Android com Android 6.0.1/ 7.0 e 8.1 (Oreo).

* **Versão 1.4.23:**

   * O TVSDK 1.4.23 foi certificado para dispositivos Android com Android N.

* **Versão 1.4.18:**

   * O Primetime foi certificado para o Amazon Fire TV.
   * O VPAID 2.0 é compatível somente com dispositivos com Android 4.0 e superior.

## Problemas resolvidos no 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Todos os clientes de TVSDK que usam CRS são altamente incentivados a atualizar para TVSDK 1.4.39 ou mais recente no iOS e Android. Essa atualização é uma substituição suspensa da implementação do aplicativo existente. Após a atualização, verifique as solicitações do URL criativo do CRS em uma ferramenta de proxy (por exemplo, Charles) para verificar se a versão no caminho reflete a versão 3.1. Por exemplo:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versão 1.4.43**

* Ticket #27143 - Não é possível reproduzir faixa de áudio 5.1 em dispositivos FireTV

   * O TVSDK agora pode reproduzir áudio AC3 em dispositivos FireTV. A reprodução está sempre em estéreo.

* Tíquete #33902 - Entrega de anúncio segura em HTTPS

   * O Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios do primetime e CRS em https.

* Tíquete #34493 - Atraso de áudio Bluetooth

   * Adicionado `alwaysUseAudioOutputLatency` na classe MediaPlayer que, quando definida, resultará no uso da latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

* Ticket #34949 - Nova versão da biblioteca de heartbeat de vídeo (VHL) integrada.

**Versão 1.4.42 (1791)**

* Zendesk #33719: FireTV 4k Adaptive Bitrate dimensiona lentamente. Adição de suporte para ABR para dispositivos FireTV 4K.
* Zendesk #33338: resetDRM apaga todos os dados do aplicativo.  Foi tratado um caso extra em que as exceções em threads não-TVSDK estavam causando o preenchimento das filas de operação do TVSDK.

**Versão 1.4.41 (1776)**

* Zendesk #33002 - Dados de ativos de companhia do TVSDK no Fire TV. Implementação de uma nova classe AdBannerAsset que retornará os dados de companhia como Lista &lt;adbannerasset> e AdAsset::id agora é uma Cadeia de caracteres em vez de longa.
* Zendesk #32821 - O jogador do Android Primetime congela quando encontra o Carimbo de Data e Hora da Apresentação (PTS) para a WWE. Esse problema foi corrigido nesta versão.
* Zendesk #33572 - Falha no início do anúncio do VideoAnalyticsProvider. O uso da combinação correta da versão de SDK conjunto VHL+Nielsen do VideoHeartbeat.jar corrigiu esse problema.
* Zendesk #33355 - Fire TV: Scrub back 15 Second Issue. Nenhuma correção do lado do TVSDK e do cliente está verificando isso na sua empresa e em terceiros.

**Versão 1.4.40 (1764)**

* Zendesk #33068 - problema de sincronização labial do Amazon no novo dispositivo. O problema de sincronização labial é corrigido nesta versão.
* Zendesk #32215 - Problemas de Segurança do Android TVSDK 1.4.38 `[Hotlist]`. Atualização para o OpenSSL-1.1.0 e curl-7.55.1 mais recentes.
* Zendesk #32920 - Tela em branco dentro de um Ad break e sem conclusão de Ad break. Correção de um problema em que um contêiner VPAID podia entrar em um estado suspenso e tratar um problema em que os anúncios VPAID do Facebook frequentemente retornavam vários blocos CDATA em um único nó \&amp;lt;AdParameters\&amp;gt; VAST.

**Versão 1.4.39 (1744)**

* Zendesk #28976 - Solicitação de licenciamento leva mais de um segundo. Enquanto as chamadas de solicitação de licença DRM que usam POST estão em execução, Curl adiciona o cabeçalho extra &quot;Expect: 100-continue&quot;. O cabeçalho &quot;Esperar:&quot; foi removido no TVSDK.
* Zendesk #27707 - Ambientes da CSAI que não respeitam os marcadores CUE IN para retorno antecipado ou retorno ao conteúdo. Forneceu suporte para vários geradores de oportunidades.

**Versão 1.4.38 (1722)**

* Zendesk #21590 - Desempenho e Rastreamento de Vídeo nos Builds Mais Recentes do Origin

Integração e certificação do VHL 2.0 no TVSDK para reduzir a barreira na implementação da VideoHeartbeatsLibrary, diminuindo a complexidade das APIs.

* Zendesk #29688 - Suporte para clientes do Android O Beta.

Suporte TVSDK para a nova versão Beta do Android.

**Versão 1.4.36 (1713)**

* Zendesk #27392 - Ignorar conteúdo no Android

Para acomodar a descriptografia, o Android TVSDK estava ampliando incorretamente o intervalo de bytes do conteúdo não-iframe em 16 bytes. O alargamento é necessário para fluxos Iframe, mas não para fluxos não-iframe.

**Versão 1.4.34 (1702)**

* Zendesk #27638 - Vazamento no objeto cURL INet

O objeto Posix cURL INet estava vazando enquanto segurava o gerenciador de compartilhamento e o cache DNS usado nas conexões cURL.

Esse problema foi resolvido excluindo o objeto Posix cURL INet do desconstrutor INet.

**Versão 1.4.33 (1694)**

* **Biblioteca OpenSSL**

A biblioteca OpenSSL foi atualizada com a versão 1.0.2j do OpenSSL.

* Zendesk #21701 - Envie o URL criativo original para a solicitação 1401 CRS em vez do URL normalizado.
Esse problema é resolvido enviando os URLs criativos originais.

* Zendesk #25023 - Reprodução de vídeo de longa duração: congelamento de vídeo, oscilações de tela Esse problema foi resolvido definindo as dimensões máximas do formato de vídeo para dispositivos set-top box CenturyLink.

* Zendesk #27460 - A nova conta Akamai não pode lidar com uma solicitação POST cdn.
O código foi atualizado para fazer o `cdn.auditude.com` solicitação de anúncio para ser GET em vez de POST.

* Zendesk #28245 - O estado de reprodução não é notificado corretamente quando o aplicativo vai do plano de fundo para o primeiro plano Esse problema foi resolvido restaurando corretamente o estado de reprodução para reproduzir ou pausar quando o aplicativo retorna para o primeiro plano.

**Versão 1.4.32 (1682)**

* Zendesk #25779 - Vulnerabilidade de segurança encontrada com o TVSDK Android 4.2 e versões anteriores tem uma vulnerabilidade de segurança quando o JavaScript é ativado em um WebView. O uso do WebView por TVSDK foi desativado para dispositivos que executam o OS 4.2 ou inferior. Isso desativa o uso de anúncios VPAID no TVSDK nesses dispositivos.

* Zendesk #26890 - Problema no estado da TELA (ATIVADO/DESATIVADO) manipulação Ref. Player Quando o mecanismo de vídeo Adobe (AVE) sai do estado SUSPENDED, o DefaultMediaPlayer não atualiza seu status. Como resultado, o DefaultMediaPlayer permanece em um estado SUSPENSO mesmo que o AVE esteja em um estado REPRODUZINDO. Esse problema foi resolvido definindo o estado DefaultMediaPlayer como PLAYING ao receber um status PLAY do AVE, mesmo que o status atual do DefaultMediaPlayer seja SUSPENDED.

**Versão 1.4.31 (1675)**

* Zendesk #21974 - Exceções devido a objetos nulos
   * AdIndex raramente é incrementado quando é nulo. Isso pode ocorrer devido a chamadas de API incorretas recebidas para o adBreak precedente. Correção dos tipos de dados para evitar essas exceções

* Zendesk #24714 - Desativar registro irrelevante
   * Atualização do TVSDK para desativar o registro irrelevante

* Zendesk #24488 - Problemas de sincronização AV no Fire TV
   * Corrigido ao melhorar o manuseio dos threads do decodificador de AV. Especificamente, sempre que as filas de quadros de entrada ou saída forem modificadas, a thread do decodificador específica para o tipo de conteúdo do quadro será executada.

* Zendesk #26551 - Corrigir as falhas do CRS
   * Quando a solicitação é HEAD (http head), não precisamos ler o conteúdo, pois ele está vazio. Embora não haja problema em tentar lê-lo, o Android antigo (4.0.x) trava enquanto chamamos read() e o Android mais recente retorna o valor correto (-1) quando chamamos read(). Com base nisso, o código foi alterado para não ler o conteúdo de &quot;head&quot;

* Exceção de ponteiro nulo do Zendesk #26696 ao acessar o TrickPlayManager
   * Correção verificando se o objeto TrickPlayManager não é nulo antes de usá-lo.

**Versão 1.4.30 (1659)**

* Zendesk #22675 A duração do ativo não é atualizada para fluxos Live/Linear Esse problema foi resolvido fornecendo uma nova API, assetDuration, em PTVideoAnalyticsTrackingMetadata que fornece a duração do ativo para fluxos Live e Linear.

* Zendesk #25853 Vazamento de memória no TVSDK ao alternar canais O problema em que um vazamento de buffer de leitura de arquivo quando o MediaPlayer é redefinido ou liberado ao baixar um arquivo foi resolvido.

**Versão 1.4.29 (1653)**

* Zendesk #21200 - O player não se recupera do estado suspenso quando o aplicativo estava em segundo plano Quando o player foi suspenso depois que a troca de transmissão foi sinalizada, a resolução permite que o player execute a troca de transmissão ao restaurar o player do estado suspenso, em vez de restaurar para a posição anterior.

* Zendesk #23412 - O player está preso a uma caixa preta se você clicar em qualquer anúncio nos últimos 3s do ad break. Este problema é o mesmo que o Zendesk #21200.

* Zendesk #23616 - O ad break ignorado busca muito longe no futuro Dependendo do tipo de inserção de anúncio (inserir/substituir), o TVSDK determina se a duração do anúncio é usada no cálculo para determinar o ponto final do ad break.

* Zendesk #25078 - Vazamento de memória DRM TVSDK no Android TV STB O vazamento de memória para o objeto adaptador DRM foi localizado e corrigido.

* Zendesk #25067 - Falha no VideoEngineTimeline Isso está acontecendo porque os objetos não foram limpos corretamente e os eventos foram chamados depois que os objetos foram destruídos. O problema foi resolvido adicionando verificações para evitar exceções nulas.

* Zendesk #25352 - Definir cabeçalho HTTP personalizado Esse problema foi resolvido adicionando um novo cabeçalho personalizado à lista de permissões no TVSDK.

* Zendesk #25617 - Sobreposição de PTS em tempo real que causa descontinuidade do player e falha de memória Esse problema foi resolvido adicionando um tratamento de sobreposição de PTS em FragmentedHTTPStreamer quando uma sobreposição ocorre no meio de um segmento.

**Versão 1.4.28 (1637)**

* Zendesk #23618 - Os eventos de ad break são acionados antes que a política de publicidade seja consultada Esse problema foi resolvido não acionando os eventos AD_BREAK_START e AD_START quando o anúncio é ignorado por causa do adForgiveness. O evento AD_BREAK_SKIPPED é enviado.

**Versão 1.4.27 (1631)**

* Zendesk #23174 - Problema de desempenho ao redimensionar o vídeo Esse problema foi resolvido fornecendo uma nova API, MediaPlayerView.setSurfaceFixedSize, que permite que o TVSDK acesse SurfaceHolder.setFixedSize() do MediaPlayerView.

* Zendesk #24450 - TVSDK faz solicitações de anúncios duplicadas Este problema ocorreu quando o tempo decorrido foi convertido em longo e não duplo, e este problema foi corrigido.

**Versão 1.4.26 (1627)**

* Zendesk #21436 - atualização da biblioteca OpenSSL para a versão 1.0.2h Atualização da biblioteca OpenSSL para OpenSSL versão 1.0.2h
* Zendesk #23825 - Os cookies não estão sendo incluídos nos retornos de chamada Corrigidos ao fornecer suporte para cookies do Android.

**Versão 1.4.25 (1620)**

* Zendesk #22900 - O fluxo do Live Adobe Primetime DRM não está sendo reproduzido no reprodutor de referência do Android O problema de alocação de memória foi corrigido.
* Zendesk #23176 - O aplicativo trava quando está tentando reproduzir anúncios VPAID O travamento ocorreu porque o aplicativo não cria uma visualização de anúncio personalizada para renderizar um anúncio VPAID. Esse problema foi resolvido ignorando os anúncios VPAID na resposta do servidor de publicidade quando não havia visualização de publicidade personalizada.

* Zendesk #23153 - SampleAES DRM Stream - Playback stalling in the TVSDK Reference Player Este problema é o mesmo que Zendesk #22900.

**Versão 1.4.24 (1612)**

* Zendesk #20784 - Analytics: ativação de conclusões de conteúdo para transições de vídeo ao vivo Esse problema foi resolvido adicionando uma API (trackVideoComplete) para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo ao vivo/linear.

* Falha de Zendesk #21977 VideoEngineTimeline durante operação placeAdBreak/acceptAd
   * Nesta edição, as seguintes bibliotecas foram atualizadas:
      * Biblioteca do AdobeMobile para a versão 4.10.0
      * Biblioteca do VHL para a versão 1.5.6
      * Biblioteca VHL-Nielsen para a versão 1.6.7

Esse problema foi resolvido adicionando uma verificação nula antes de adicionar anúncios à lista de anúncios aceitos.

* Zendesk #22313 A taxa de bits para os STBs com chipset Amilogic não vai além de 1,2M Esse problema foi resolvido pré-carregando os recursos de codec de mídia e desabilitando o switch ininterrupto para dispositivos de chipset Amilogic.

* Ativo AES HLS de amostra do Zendesk #19520 não reproduzido em players TVSDK Esse problema foi resolvido ao manipular vários descritores PMT para fluxos HLS criptografados AES de amostra.

**Versão 1.4.23 (1602)**

* Zendesk #18852 - Atualizar a lógica de seleção criativa com base nas regras CRS Esse problema foi resolvido adicionando um arquivo de configuração JSON para especificar a prioridade da seleção criativa.

* Zendesk #20861 - Android N Esta versão oferece suporte para Android N, removendo a capacidade de usar diretamente as bibliotecas nativas da plataforma Android que não estão mais acessíveis para aplicativos que são executados no Android N.

* Zendesk #21018 - Android N crash Mesma resolução que ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter trava em um erro Invalid_Key O erro Invalid_Key não inclui uma descrição do AVE, portanto, a análise do texto resultou em NPE. O problema foi resolvido adicionando uma verificação nula para a descrição durante onError antes de analisar a descrição.

* Zendesk #22286 - A biblioteca nativa está alocando memória lendo chave/fragmento causando falha Esta falha que ocorreu no Android ao tentar carregar um manifesto com várias chaves simultaneamente foi corrigida.

**Versão 1.4.22 (1581)**

* Zendesk #17236 - Tempo de cabeçalho de reprodução não confiável para vídeos HLS com DRM O salto de tempo com os fluxos LBA, onde o tempo de início do segmento de áudio não corresponde ao tempo de início do segmento de vídeo, foi corrigido.

* Zendesk #17680 - A reprodução de vídeo está congelando na caixa Selevision Andredo O decodificador de vídeo neste dispositivo às vezes retorna um salto de tempo de saída significativo ao desenfileirar o quadro de vídeo do buffer de saída, e esse carimbo de data e hora de saída permanece alto. Esse problema foi resolvido retornando um *perfil de vídeo não suportado* erro que não força o reprodutor a tentar novamente o mesmo perfil ou escolher um perfil diferente.

* Zendesk #19074 - Congelamento de vídeo durante reprodução de truques FFWD e REW Esse problema foi resolvido adicionando um novo aviso TRICKPLAY_ENDED_DUE_TO_ERROR para notificar o aplicativo que o trickplay foi encerrado e que o vídeo foi pausado devido a um erro irrecuperável.

* Zendesk #19574 - TVSDK não retorna dados de resposta do M3U8 para conteúdo DRM ou não DRM Esse problema foi resolvido das seguintes maneiras:

* Zendesk #19986 - Comportamento OP interrompido para certos dispositivos como Android TV
* Adicionando um erro FILE_NOT_FOUND à condição.
* Quando o erro vem de uma *arquivo não encontrado* erro, separando o URL e a resposta da descrição do erro se a resposta estiver disponível.
O erro lógico introduzido pelo suporte ao NVidia shield OP foi corrigido. Em dispositivos de blindagem que não sejam NVidia, confie nos sinalizadores de segurança de exibição mesmo quando o tipo de exibição for desconhecido.

* Zendesk #20549 - Manuseio de listas de reprodução obsoletas. Esse problema foi resolvido reduzindo o intervalo entre a atualização ao vivo do manifesto para a metade da duração do segmento esperada, se a busca anterior não receber novos segmentos.

* Zendesk #20742 - O uso da memória parece continuar a aumentar ao reproduzir conteúdo ao vivo no FireTV. O travamento é causado pela tabela de referência de objetos JNI que atingiu o limite. Esse problema foi resolvido excluindo a referência ao objeto MediaFormat que foi criado durante a reinicialização do decodificador.

* Zendesk #21125 - Retorno de ad break ao vivo/linear com antecedência (CSAI). Adição de um recurso que permite ao reprodutor retornar ao conteúdo principal durante um ad break caso registre a junção em dicas de anúncio usando a junção no detector de oportunidades.

* Zendesk #21334 - Valor de tempo limite de solicitação de anúncio TVSDK para solicitação de anúncio de terceiros. Uma configuração adRequestTimeout foi adicionada a AdvertisingMetadata que permite um tempo limite global para a chamada de anúncio.

**Versão 1.4.21 (1566)**

* Zendesk #17781 - captura de tela do ADB que não funciona Esse problema foi resolvido adicionando a API DefaultMediaPlayer.create(Context context, boolean secureSurface), que permite captura de tela.
Para permitir capturas de tela, passe falso para secureSurface.
Importante: recomendamos que você não ative esse recurso de captura de tela em uma configuração de produção.

* Zendesk #19074 - Congelamento de vídeo durante a reprodução de truques FFWD e REW Os seguintes problemas que ocorreram quando o trickPlay podia congelar na reprodução foram resolvidos:

* Zendesk #19532 - As legendas ocultas parecem fora de ordem
   * O FHS inicia o trickplay, mas o primeiro segmento do iframe não tinha um quadro nele.
   * Ao baixar um segmento do iframe, se o FHS atingir uma condição de erro, ele sairá do trickplay e pausará a reprodução.
   * A implementação do MediaCodec aguarda sempre a disponibilidade da fila de entrada, enquanto é solicitada a liberação de todos os buffers de entrada/saída.
Esse problema foi resolvido invertendo a ordem das dicas de WebVTT para que várias dicas sobrepostas parecessem &quot;rolar para cima&quot;.

* Zendesk #19574 - O TVSDK não retorna dados de resposta do M3U8 para conteúdo DRM ou não DRM No carregamento inicial do arquivo de manifesto em PTMediaPlayerItem.prepareToPlay, se o carregamento falhar, o TVSDK não relatará o corpo da resposta de falha para o aplicativo.
Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro ao aplicativo.

* Zendesk #19701 - Congelamento da reprodução com SAP/Discontinuity O congelamento do player quando o áudio e o vídeo são desalinhados na descontinuidade foi resolvido.

* Bug #PTPLAY-11162 - A atualização da biblioteca OpenSSL para a versão 1.0.2f foi resolvida.

**Versão 1.4.20 (1546)**

* Zendesk #17384 - Solicitação de recurso: O suporte de metadados ID3 para reprodução AAC Suporte para tags ID3 na mídia AAC foi fornecido no TVSDK para Android a partir da versão 1.4.20.

* Zendesk #18358 - O jogador congela no switch de taxa de bits com descontinuidades fora de sincronia Esse problema foi resolvido manipulando os casos de borda de costura ABR apropriadamente.

* Zendesk #19232 - O aplicativo que usa o TVSDK 1.4.18 está se comportando de forma estranha com o Amazon OS versão 4 mais antigo. Esse problema foi resolvido com a remoção da criação de exibições da Web ocultas no processo de inicialização do reprodutor TVSDK para evitar conflitos com dispositivos que não são compatíveis com o Android Webview.

* Zendesk #19585 - Reprodução em câmera lenta quando ocorre a transição da taxa de bits adaptativa.
Durante a alternância ABR, se o novo perfil tiver uma taxa de amostra de áudio diferente do perfil atual, a reprodução se tornará rápida ou em câmera lenta. Isso ocorre porque o apresentador de vídeo não é notificado de que o formato de áudio foi alterado.
Esse problema foi resolvido verificando se o sinalizador de notificação está definido no lugar correto.

* Zendesk #19683 - SAP DAI playback - Sem áudio por alguns segundos.
Para vários casos na lógica do TVSDK, quando o carimbo de data e hora de dois segmentos de representação foram comparados, RENDITION_TIMEOUT_THRESHOLD foi usado como um intervalo aceitável de valor, pois o carimbo de data e hora nem sempre pode ser combinado com uma diferença de 0 ms. Se a lacuna estiver dentro do intervalo de RENDITION_TIMEOUT_THRESHOLD, presume-se que seja uma correspondência.

O RENDITION_TIMEOUT_THRESHOLD foi definido como 100 ms, mas foi considerado insuficiente para determinados fluxos. Esse problema foi resolvido aumentando o RENDITION_TIMEOUT_THRESHOLD para 200 ms.

* Zendesk #19699 - O TVSDK falha ao alternar entre faixas de legendas em VTT Esse problema foi resolvido fazendo o despejo do player e recarregando o manifesto quando uma faixa é alterada e corrigindo o problema de conversão de sequência de caracteres UTF8 que afetava os nomes de faixas de legenda WebVTT de dois bytes.

* Zendesk #19717 - CC options display issue Esse problema foi resolvido manipulando corretamente a sequência de caracteres Unicode.

* Zendesk #19910 - TIT2 ID3 tags não sendo detectadas Esse problema foi resolvido fornecendo suporte mais completo para codificações de sequência ID3 v2.4 e suporte para ID3 v2.3.

* Zendesk #20135 - O TVSDK está acionando vários onComplete para conteúdo de VOD.
Esse problema foi resolvido adicionando o ouvinte de eventos post_roll_complete no local certo, em vez de no caso completo do evento de alteração de status.

**Versão 1.4.19 (1521)**

* Zendesk #4180 - O TVSDK não está aplicando o HDCP.
   * Essa é uma correção parcial para esse ticket e aborda apenas o problema dos dispositivos NVidia shield.
Você deve usar a API de detecção de HDCP implementada corretamente no Nvidia Shield para rastrear dinamicamente o status do HDCP.

* Zendesk #18358 - O TVSDK congela no switch de taxa de bits com descontinuidades fora de sincronia.
   * Esse problema foi resolvido adicionando um novo aviso para detectar a descontinuidade do PTS e forçando a verificação do PTS a refazer a pesquisa do segmento correto para cada switch ABR.
Para corrigir o congelamento, a chamada para o método mediaPlayer.setCustomConfiguration deve incluir forcePTSCheckForABR como argumento.

* Zendesk #19038 - Não há transmissão ao vivo no Asus Zenpad 10.

  Esse problema foi resolvido pré-carregando as informações do codec de mídia, para que você não consulte a função em tempo de execução.

* Os seguintes problemas são os mesmos do Zendesk #19038:
   * Zendesk #19483 - O TVSDK está travando na plataforma Intel.
   * Zendesk #19171 - Falhas no Asus Memo Pad 7 com Android 5.0.

**Versão 1.4.18 (1503)**

* Zendesk #3324 - Os relatórios de anúncios do Primetime não rastreiam ad breaks quando não há mídia de anúncio em um VMAP.
Quando um ad break está vazio, o início do ad break e os eventos de rastreamento de conclusão não eram tocados. Esse problema era resolvido enviando pings de início de ad break em ad breaks vazios, como VMAP AdBreak, com um nó AdSource válido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) é ignorado após a chamada MediaPlayer.reset() Esse problema foi resolvido adicionando setCCVisibility(Visibility.INVISIBLE); à função reset() na classe MediaPlayer.

* Zendesk #18328 - Problema de quadro descartado em dispositivos Amazon Fire TV 2nd gen para o conteúdo com 60FPS Este problema foi resolvido aplicando o FPS codificado para a tomada de decisão do tempo de sono e com uma lógica de previsão FPS melhor codificada.

**Versão 1.4.17 (1472)**

* Zendesk #2231 - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification Esse problema foi resolvido incluindo o corpo de resposta do manifesto quando há um erro de análise.

* Zendesk #17703 - VideoEngineView não impede capturas de tela durante a reprodução do vídeo O método setSecure está disponível desde a API 17, mas como a API 17 abrange 4.2, 4.2.1 e 4.2.2, não se sabe qual acionará uma exceção ou se é específica do dispositivo. Esse problema foi resolvido vinculando VideoEngineView.setSecure à cláusula try catch.

* Zendesk #17919 - A busca de conteúdo causa erro de heartbeat Um erro de Posição de dados de entrada inválido estava ocorrendo como resultado da chamada de heartbeat gerada quando a busca era iniciada após a pré-exibição. Esse problema foi resolvido.

**1.4.16a** (1454-A)

* Zendesk #18215 - Alguns fluxos AES não são capazes de carregar.
Esse problema foi resolvido verificando o tamanho dos metadados do DRM do perfil antes de carregar a chave AES.

**Versão 1.4.16 (1454)**

* Zendesk #3875 - Tab S Trava durante a reprodução Revertendo a dependência do OKHTTP no Auditude para CRS porque o TVSDK agora está usando diretamente httpurlconnection em vez de curl. O problema foi resolvido limpando as exceções antes de fazer qualquer outra chamada JNI.

* Zendesk #4487 - Rastreamento do canal linear de conteúdo O problema foi resolvido permitindo a reinicialização do rastreador de heartbeat de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17919 - Android - busca de conteúdo causa erro de pulsação O problema quando a pulsação está em um estado de erro quando há uma busca em um capítulo foi resolvido.

* Zendesk #18053 - Adobe Primetime falha em Marshmallow O TVSDK estava travando no Android M OS quando a biblioteca TVSDK usou o código neon que faz a conversão YUV -> RGB de cores. O problema foi resolvido atualizando as funções que estão causando esse problema usando a versão não neon do código.

* Zendesk #18072 - Android M - Falha do aplicativo Ao verificar se o perfil e o nível são compatíveis, ocorre uma falha ao chamar as APIs MediaCodecList e MediaCodecInfo. O problema foi resolvido fornecendo uma solução temporária, carregando todas as informações do codec antecipadamente para evitar a chamada dessas APIs somente quando as informações do codec forem necessárias.

* Zendesk #18074 - Legendas em árabe que não funcionam no Nexus com Android 6.0 O problema foi resolvido fornecendo suporte ao mapa de fontes CTS para Android.

**Atualização da versão 1.4.15 (1438)**

* Zendesk #17437 - Longo atraso na inicialização de conteúdo de VOD com alguns fluxos AES.
Para resolver esse problema, se várias chaves estiverem listadas no manifesto, baixe todas as chaves AES em paralelo.

**Versão 1.4.15 (1435)**

* Zendesk #4278 - Falhas no Android set top boxes quando a taxa de bits adaptável muda (ABR).
A correção foi adicionar suporte para o switch ABR ininterrupto com o codec de mídia Android mais recente.

* Zendesk #17063 - Chamar mediaPlayer.reset() causa um erro de redefinição do mecanismo de vídeo.
A correção era incluir o MediaErrorCode original de VideoEngineExceptions ao despachar ErrorEvents.

* Zendesk #17130 - Uma pausa breve, mas perceptível ao alterar a taxa de bits vista no FireTV.
(Igual ao #4278 acima) A correção foi adicionar suporte para switch ABR ininterrupto com o codec de mídia Android mais recente.

* Zendesk #17666 - Marcadores de anúncios adicionais, Inesperado ou Sem anúncios ao retomar o conteúdo.
A correção era um problema ao fazer o conteúdo prepareToPlay on video-on-demand (VOD), a busca inicial é executada no horário local em vez de no tempo virtual.

* Zendesk #17437 - Longo atraso na inicialização de conteúdo de VOD com alguns fluxos AES.
A correção era baixar todas as chaves AES em paralelo quando várias chaves eram listadas no manifesto.

* Zendesk #17851 - Android TV - Quadro Preto durante ABR A correção foi especificar KEY_MAX_WIDTH e KEY_MAX_HEIGHT para ativar a reprodução adaptável.

**Versão 1.4.14 (1415)**

* Zendesk #3875 - Tab S Trava durante a reprodução.
Uma correção adicional foi necessária para evitar a falha.

* Zendesk #17245 - Fallback no Android TV não está funcionando.
Correção de um problema adicional em que a reprodução trava quando o fallback é ativado e a resposta do VMAP tem um ad break vazio.

**Versão 1.4.14 (1412)**

* Zendesk #17245 - Fallback no Android TV não está funcionando.
Remoção de uma restrição para desabilitar o reempacotamento criativo em anúncios de fallback.

**Versão 1.4.13 (1388)**

* Zendesk #3502 - Suporte a failover baseado em cliente HLS durante um ad break Permite failover para o manifesto principal ao atualizar o erro de perfil ao vivo ocorre durante o período de ad break.

* Zendesk #3875 - Tab S Trava durante a reprodução Para resolver o conflito entre HttpUrlConnection e cURLm, use uma biblioteca de terceiros.

* Zendesk #4450 - problema ao configurar metadados personalizados para uma única inserção em um resolvedor de conteúdo Adicionar um setter às configurações de Oportunidade.

**Versão 1.4.12 (1388)**

* Zendesk #2751 - CSAI e CRS | Aprimorar: trate elementos dinâmicos em determinados URLs de arquivo de mídia.
Serviço de reempacotamento criativo atualizado para lidar adequadamente com anúncios com URLs criativos dinâmicos.

* Zendesk #3965 - Alternar de volta para a reprodução normal a partir de trickplay resulta em um salto para frente um pouco antes de iniciar a reprodução.
   * Correção inclui TVSDK que retorna o tempo antes da alteração da taxa até que todas as variáveis sejam atualizadas, em vez de tentar calcular GetStreamTime.
   * Correção de uma falha ao alterar a velocidade de execução do truque próximo ao final do fluxo.
   * Cálculo do tempo atual corrigido durante a execução do truque.

* Zendesk #3978 - Truckplay às 8x e 16x frequentemente congela.
   * Sempre escolha o perfil de jogo de truque com a menor taxa de bits para evitar buffering constante.
   * Aumente o intervalo de salto de quadros para obter uma alta taxa de truques.
   * Correção de um problema em que o buffer continua a crescer depois de atingir sua duração alvo durante a execução de um truque.

* Zendesk #3992 - Velocidades adicionais do Trickplay.
O TrickPlay foi atualizado para aceitar taxas superiores a 16x; +/- 32, +/- 64 e +/- 128 também são agora permitidos.

* Zendesk #4007 - Interpretação do objeto GEOB como parte dos metadados da linha do tempo (Android e Web).
Adição da API setByteArray e getByteArray.

* PTPLAY-7301 - Início instantâneo no ponto de acesso aleatório.
A Ativação instantânea foi atualizada para permitir um ponto de partida diferente de zero.

**Versão 1.4.11 (1363)**

* Zendesk #2076 - Gagueira frequente ao reproduzir vídeo no Motorola Xoom com Android 4.0.3 Adição de dispositivos ao lista de permissões para evitar que eles tentem reproduzir conteúdo de alto perfil.

* Zendesk #2197 - `[Ads]` Rastreamento de erros de anúncio despacham OperationFailedEvent com notificação de aviso.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro não preenchida
   * o código de erro 400 será exposto se o anúncio em linha tiver criação incorreta.
   * `[ERRORCODE]` a macro será codificada em URL

**Versão 1.4.10 (1354)**

* Zendesk #2941 - ativos ao vivo não têm &quot;0&quot; no intervalo pesquisável Anteriormente, havia um buffer de 3 segmentos ao buscar o início de um fluxo ao vivo, agora é possível buscar o início de um fluxo ao vivo (ou seja, o início do primeiro segmento).

* Zendesk #3169 - Atualizar reprodutor de referência com a integração do Adobe AnalyticsO reprodutor de referência foi atualizado com a biblioteca do Adobe Analytics como exemplo de implantação.
* Zendesk #3299 - Comportamento inexplicável de truque de jogo
   * Correção de um erro em que retornar ao estado de reprodução após interromper a reprodução de truque podia levar vários segundos (às vezes, mais de 25 segundos).
   * Correção de um erro em que invocar uma segunda reprodução de truque na mesma mídia pode fazer com que o fluxo congele no momento atual.
* Zendesk #3433 - Android e Flash - Problemas com legendas

O GetLine para WebVTT não respeitava uma &lt;cr>&lt;lf> comprimento ajustado para um pacote; a última legenda pode conter caracteres de legendas anteriores.

* PTPLAY-6243 - Aprimorar o reprodutor de referência para capturar informações de depuração

Os players de referência de amostra do Android foram aprimorados com uma opção para ativar logs de depuração e enviar os resultados por email. Essa opção é encontrada no menu Log no reprodutor de referência.

**Versão 1.4.9 (1332)**

* Zendesk #2649 - Buffer Concluído ocorre antes que o buffer inicial esteja cheio

Após uma busca, possível caso em que o mecanismo de vídeo define o estado como REPRODUZINDO antes do apresentador de vídeo estar pronto para ser reproduzido. Ocorre quando o estado do buffer é alto antes da busca. Corrija notificando o mecanismo de vídeo sobre o estado de buffer baixo. Com o mecanismo de vídeo em estado de buffer baixo, chamar Reproduzir faz com que o estado mude para BUFFERING em vez de PLAYING. A reprodução continua quando o estado muda para REPRODUZINDO.

* Zendesk #2846 - Solicitação de aprimoramento: Fornecer a capacidade de definir diferentes sequências de agente-usuário para chamadas feitas pela biblioteca Auditude

Uma nova API foi adicionada para definir o agente do usuário para chamadas relacionadas a anúncios, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Se nenhum agente do usuário for definido, o padrão será usado. Isso só afeta o agente do usuário para chamadas relacionadas a anúncios. O agente do usuário para chamadas de mídia permanece inalterado, o que é &quot;Adobe Primetime&quot;+&lt;default useragent=&quot;&quot;>.

**Versão 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Erro com local ... Se o carregamento do manifesto em FragmentedHTTPStreamer::ThreadParseManifest() falhar, verifique se o domínio do URL é localhost e, em caso positivo, altere o domínio para 127.0.0.1 e recupere o ThreadParseManifest.
* Zendesk #3072 - Mudança automática para taxas de bits mais baixas. Alteração do cálculo do comprimento do buffer para ignorar carga PTS zero.
* Zendesk #3168 - WebVTT legendas exibidas apenas para os primeiros 10 segundos.
* Zendesk #3193 - Solicitação de uma API de alteração de perfil em TVSDK, PlaybackEventListener.onProfileChanged() foi adicionado.

**Versão 1.4.7 (1311)**

* Zendesk #2197 - Rastreamento de erros de anúncios. Adicionada notificação para falha do ativo ao carregar o manifesto
* Zendesk #2575 - PSDK ignora anúncio personalizado em fluxo do MARK antes do vídeo
* Zendesk #2719 - Win Death com anúncios auditude, rastreamento de beacon fixo quando redirecionado para URL relativo no plug-in auditude
* Zendesk #2760 - tag DISCONTINUITY ignorada durante o modo TrickPlay
* Zendesk #2805 - Falha do player no início da reprodução, mesma correção que Zendesk #2719
* Zendesk #2817 - Android player - O player às vezes trava e para de jogar, corrigido estendendo os buffers de decodificação de 2.0 para 3.0 segundos
* Zendesk #2839 - O Adobe Primetime PSDK suporta chipsets ARMv8?, correção adicionada para o travamento encontrado no Galaxy S6.
* Zendesk #2885 - Auditude Falha na reprodução, mesma correção que Zendesk #2719
* Zendesk #2895 - Falha de HLS ao vivo consistentemente após 10 minutos de reprodução
* Zendesk #2925 - Feedback em relação ao Android dev build (1.4.5), em certos dispositivos quando enfileiramos o pacote para a fila de entrada, se o PTS for negativo, o decodificador entra em um estado estranho que sempre obtemos um PTS de saída negativo para pacotes futuros. A correção definirá o PTS de entrada como zero se for negativo para evitar esse problema.
* PTPLAY-4645 - Desative o suporte à cifra RC4 em openssl. Há explorações conhecidas para RC4. Isso significa que, se for feita uma tentativa de conexão com um servidor que só oferece suporte a RC4, ela falhará.

**Versão 1.4.6 (1282)**

* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede precárias, corrigidas com a remoção da implementação de switch rápido.
* Zendesk #2631 - Legendas em árabe no Android: o texto em várias linhas aparece cortado, corrigido ajustando o tamanho da fonte para fontes em árabe.
* Zendesk #2844 - Buffering na Nota 4 e o tempo de download do fragmento não são precisos.

Esse problema foi corrigido adicionando-se a latência entre downloads de segmentos de vídeo no cálculo da largura de banda e fazendo com que a lógica de cálculo do tempo de download usasse o tempo de ciclo de solicitação completo.

* Zendesk #2908 - Legendas em árabe não funcionam no Nexust 5, 6 e 7, corrigidas adicionando mais 2 fontes substitutas para scripts em árabe.
* PTPLAY-4627 - atualização do appsdk Nielson para a versão 1.2.3.7
* PTPLAY-5084 - Suporte ao failover de atualização de Live Master Manifest

**Versão 1.4.5 (1248)**

* Zendesk #1757 - Apenas áudio reproduzido ou falha do player para algum perfil de taxa de bits de vídeo, falha do Nexus 4 e Nexus 7 corrigida
* Zendesk #2072 - TimedMetadata para AdEvent não contém o URL completo apenas &quot;http&quot;
* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede precárias
* Zendesk #2256 - Acesso à Lista de Reprodução Mestra, PSDK atualizado para enviar eventos timedMetadata para tags assinadas na lista de reprodução mestre.
* Zendesk #2269 - Duas línguas de legendas diferentes aparecem na tela ao mesmo tempo com WebVTT
* Zendesk #2417 - Player tentando baixar legendas antes do início da reprodução, WebVTT estava usando a variável de número de segmento errada para correspondência de número de segmento. O bug só era exibido para mídias que tinham índices de segmento começando em zero.
* Zendesk #2470 - PSDK não retorna do estado SUSPENSO quando a alteração da taxa de bits ocorre após a suspensão. Em uma situação especial, quando a busca inteligente é chamada por RestoreGPUResource (restaurar player do estado suspenso) e o switch de fluxo detectado antes disso, a busca inteligente não pode ser concluída e resulta em buffering constante.
* Zendesk #2451 - Closed Caption &quot;bottomInset&quot;, parâmetro &quot;bottomInset&quot; adicionado ao código de legenda
* Zendesk #2480 - desabilitando a otimização de redirecionamento HTTP 302, Adição de suporte para configuração da propriedade useRedirectUrl
* Zendesk #2486 - sinais de terceiros
* Zendesk #2547 - Árabe legendas: O texto deve ser alinhado à direita justificado

**Versão 1.4.4 (1195)**

* Zendesk #1158 - Falha na reprodução no Huawei Valiant (Y301A1)
* Zendesk #1709 - Tamanho de mídia incorreto e vídeo ampliado
* Zendesk #1757 - Somente áudio reproduzido após alternância de perfil entre fluxos com dados spa/pps idênticos
* Zendesk #2095 - Status HTTP 307 (redirecionamento) faz com que o reprodutor Adobe pare a reprodução
* Zendesk #2126 - Evento TimedMetaData ausente para o último ADEVENT, tags assinadas que existem após o último segmento não foram relatadas para PSDK do AVE
* Zendesk #2227 - Travamentos no VideoEngine nativeReset e nativePause
* Bug #3921755 - Atualização da biblioteca OpenSSL para a versão 1.0.1L

**Versão 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Legendas ocultas ativadas e desativadas
* PTPLAY-1818 - O jogo de truque de rebobinar pára no anúncio em vez de retroceder após ele
* PTPLAY-2736 - Uma legenda WebVTT exibida anteriormente é exibida na tela quando um fluxo com legenda WebVTT é concluído
* PTPLAY-3773 - Um anúncio intermediário não é reproduzido quando a reprodução do fluxo é iniciada após a posição do anúncio

**Versão 1.4.2**

* Zendesk #1561 - Suporte a failover baseado em cliente HLS no Primetime. Usará a data e hora do programa para tratar do failover
* Zendesk #1590 - LoadInfo.MediaDuration é sempre 0 (não corrigido apenas para áudio)
* Zendesk #1626 - Potencial Vazamento de Memória no Player. Não há vazamento de memória real, o problema ocorreu com NotificationHistory salvando as últimas 1000 notificações, isso foi reduzido para 100.
* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede precárias

**Versão 1.4.1 (1121)**

* Zendesk #1951 - Bloqueio em VideoEngine.nativeReset() em dispositivos 4.0.x
* Zendesk #2064 - Native Crash SIGSEGV em dispositivos Android baseados em intel
* Zendesk #2075 - Bloqueio em VideoEngine.nativeReleaseGPUResource em dispositivos 4.0.x Observação: esta build é &#42;&#42;&#42;obrigatório&#42;&#42;&#42; para suporte do Android 5.0 (Lollipop)
* Zendesk #1513 - Suporte ao Android Lollipop
* Zendesk #1709 - Tamanho de mídia incorreto e vídeo ampliado
* Zendesk #1871 - WebVTT legendas ocasionalmente desaparecem e reaparecem ao visualizar um livestream com legendas WebVTT
* Zendesk #1996 - Nenhum marcador de linha do tempo é visto no PSDK 1.4.0
* Zendesk #2046 - Falha com PSDK 1.4.1.1113, falha fixa para transmissões em tempo real quando nenhum anúncio é retornado do auditude
* Bug #3769657 - Atualizar a versão do curl para 7.38.0
* PTPLAY-1575 - Quando a reprodução do ABR começa com o fluxo somente de áudio e depois muda para o fluxo de áudio/vídeo, o vídeo nunca é renderizado enquanto o áudio continua
* PTPLAY-2499 - Atualização do OpenSSL para a versão 1.0.1j para solucionar vulnerabilidades recentes
* PTPLAY-2632 - O vídeo não se recupera após o anúncio intermediário concluído no Android Lollipop
* PTPLAY-2678 - Paralisações de vídeo durante testes de longevidade ao vivo no Android Lollipop

**Versão 1.4.0**

* Zendesk #1024 - Recurso para remover anúncio de transmissão via manifesto
* Zendesk #1293 - Problema De Seleção De Legendas Ocultas.
* Zendesk #1590 - LoadInfo.MediaDuration é sempre 0, mediaDuration agora está mostrando o valor correto.
* Zendesk #1629 - falhas do player/app no final da reprodução de anúncio no Galaxy S4
* Zendesk #1674 - ClosedCaption Não aparece, corrija a exibição da legenda 708 quando os códigos ETX 0x03 estiverem ausentes.
* PTPLAY-2157 - Os estilos de Legendas ocultas padrão foram retornados por getters, mesmo depois que um estilo diferente fosse definido e verificado visualmente no fluxo. As propriedades de estilo das Legendas ocultas agora mostrarão o valor para o qual foram definidas.

## Problemas conhecidos no 1.4 {#known-issues-in}

**Versão 1.4.31**

* PTPLAY-16803 - As Legendas ocultas não funcionarão com conteúdo somente de áudio, pois o sistema de legenda precisa de vídeo para funcionar. Sem vídeo, não há dimensão de visor e, sem uma dimensão de visor, não é possível exibir gráficos para legendas.
* PTPLAY-1634 - A mesma tag inscrita tem carimbos de data e hora diferentes em diferentes janelas ativas. Quando a janela dinâmica se move, a mesma tag deve ter os mesmos carimbos de data e hora. No entanto, às vezes, até mesmo as mesmas tags têm carimbos de data e hora diferentes.
* PTPLAY-3197 - Falha com sinal 11 SIGSEGV erro no dispositivo Acer Iconia após ~ 1 hora de reprodução contínua
* PTPLAY-3310 - Com algum áudio de taxa de bits mais baixa, o áudio torna-se instável / gagueira em Acer Iconia
* PTPLAY-3355 - Falha de WIN DEATH no Motorola Xoom com 4.0.x após ~ 1 hora de reprodução contínua.
* PTPLAY-3557 - O retrocesso em um ad break está causando a conclusão do fluxo
* PTPLAY-7079 - A janela de reprodução no cliente Android não funciona com Secure Stop/Hard Stop
* Bug #3760144 - A resolução pode mudar ou parecer pulsar quando o fluxo é pausado em alguns dispositivos, como Kindle Fire 7 e Samsung Galaxy Nexus. Apenas observável sob inspeção atenta
* Bug #3761170 - seekToLocal in Live with Ads não pode buscar de volta no conteúdo do anúncio, é melhor usar as APIs currentTime para fluxos ao vivo
* Bug #3763370 - Transmissões ao vivo com anúncios ocasionalmente mostrarão dois marcadores de anúncios próximos quando deveria haver apenas um. Esses marcadores representam o mesmo anúncio e somente um será reproduzido
* Bug #3763373 - O marcador de anúncio pode desaparecer brevemente ao procurar um anúncio em fluxos de VOD. O marcador de publicidade é restaurado e não há nenhum outro efeito adverso na linha do tempo
* Alguns dispositivos têm problemas conhecidos de reprodução. Consulte [Problemas conhecidos do dispositivo no 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementação de referência - a opção &quot;Truque play&quot; não está implementada no aplicativo de amostra
* Em alguns dispositivos Android TV, um quadro preto pode ser visto devido a uma redefinição do decodificador nos seguintes pontos de transição:
   * entrar e sair do modo de jogo
   * alternando entre faixas de áudio de associação tardia
   * de um anúncio para o conteúdo principal.

**Versão 1.4.23**

* As Legendas ocultas não funcionarão com conteúdo somente de áudio porque o sistema de legendas precisa de vídeo para funcionar. Sem o vídeo, não há dimensão de visor e, sem uma dimensão de visor, não é possível exibir gráficos para legendas.
* A partir da versão 1.4.23, o TVSDK não será compatível com o Gingerbread OS 2.3. Isso ocorre porque o TVSDK usou as seguintes bibliotecas privadas do Android para coletar informações de hardware sobre dispositivos com o sistema operacional Gingerbread:

   * `libstagefright.so`
   * `libcutils.so`

Na versão Android N, o Google removeu o acesso a essas bibliotecas privadas. Atualmente, o sistema operacional Gingerbread representa menos de 1% da participação no mercado global do sistema operacional Android, portanto, após a versão 1.4.23, o sistema operacional Gingerbread não será mais suportado pelo TVSDK.
Ao usar a versão 1.4.23 (que inclui suporte para Android N) ou posterior:
* Atualize seus aplicativos para usar o minSdkVersion versão 11.
* Se o usuário final estiver executando o OS 2.3, a versão do SDK será inferior à minSdkVersion do aplicativo. O sistema interrompe a instalação ou atualização do aplicativo.
* Se o usuário final estiver executando uma versão superior ao OS 2.3, o aplicativo será instalado corretamente.

Se você atualizar o minSdkVersion:

* Se o usuário final estiver executando o OS 2.3, o aplicativo está instalado, mas a reprodução não funcionará.
Isso se aplica à atualização e à instalação nova.
* Se o usuário final estiver executando um sistema superior ao OS 2.3, o aplicativo será instalado corretamente e o conteúdo será reproduzido corretamente.

**Versão 1.4.22**

* A saída antecipada dos anúncios não funciona com alguns dos anúncios intermediários quando a tag de splice-out e splice-in estão muito próximas umas das outras.

**Versão 1.4.2**

* Retroceder em um ad break está causando a conclusão do fluxo.

O Media Player envia incorretamente MediaPlayer PlayerState.Complete durante a operação de retrocesso de Truque Play, quando atinge um limite de anúncio. O reprodutor deve ignorar esse evento quando estiver no modo de execução de truque, caso contrário, o SDK manipulará o estado corretamente.

**Versão 1.4.0 (1086)**

* PTPLAY-1634 - A mesma tag inscrita tem carimbos de data e hora diferentes em diferentes janelas ativas. Quando as janelas ativas são movidas, a mesma tag em cada uma delas deve ter os mesmos carimbos de data e hora. No entanto, às vezes, até mesmo as mesmas tags têm carimbos de data e hora diferentes.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE às vezes é visto depois de vários switches para/do fluxo alternativo em blecautes
* Bug #3726865 - Se um fluxo de LBA MultiBitrate inicia a partir de um fluxo somente de áudio, o vídeo não será exibido se for alternado para um fluxo de Áudio/Vídeo. A partir de um fluxo de áudio/vídeo não exibirá esse problema e poderá alternar com êxito entre fluxos de áudio e áudio/vídeo
* Bug #3760144 - A resolução pode mudar ou parecer pulsar quando um fluxo é pausado em alguns dispositivos, como Kindle Fire 7 e Samsung Galaxy Nexus. Apenas observável sob inspeção atenta
* Bug #3761170 - seekToLocal in Live with Ads não pode buscar de volta no conteúdo do anúncio; é melhor usar as APIs currentTime para fluxos ao vivo
* Bug #3763370 - Transmissões ao vivo com anúncios ocasionalmente mostrarão dois marcadores de anúncios próximos quando deveria haver apenas um. Esses marcadores representam o mesmo anúncio e somente um será reproduzido
* Bug #3763373 - O marcador de anúncio pode desaparecer brevemente ao procurar um anúncio em fluxos de VOD. O marcador de publicidade é restaurado e não há nenhum outro efeito adverso na linha do tempo
* Alguns dispositivos têm problemas conhecidos de reprodução. Para obter mais informações, consulte [Problemas conhecidos do dispositivo no 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementação de referência - a reprodução de truques não é implementada no aplicativo de amostra.

## Problemas conhecidos do dispositivo no 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Solução alternativa |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | O atraso ABR é esperado, pois ele está reiniciando o decodificador. |  |  |
| HTC Desire (diferente de HTC Desire HD) | QSD8250 | Não é possível reproduzir o vídeo. Retorna o erro VIDEO_PROFILE_NOT_SUPPORTED. | O desejo não fornece um decodificador de hardware adequado. Ele fornece o decodificador de SW do Stagefright. | Reinicie o dispositivo. |
| HTC EVO 4G | QSD8650 | Nenhum decodificador de hardware. | A Qualcomm não tem um decodificador de hardware. | Atualize para o Android 4.x. |
| Kindle FireSystem versão 6.0 | TI OMAP4 | Não reproduz fluxos HLS. O vídeo no AIR não funciona. |  | Atualize para a versão do sistema 6.3. |
| Kindle Fire HD | TI OMAP4 | Pode entrar em um estado em que não é possível reproduzir vídeo. Retorna os erros VIDEO_PROFILE_NOT_SUPPORTED e UNRECOVERABLE_ERROR. | O decodificador de hardware entra em um estado irrecuperável quando o aplicativo não encerra totalmente o decodificador de hardware, por exemplo, depois de encontrar uma falha. Acontece em aplicativos nativos no dispositivo também. | Reinicie o dispositivo. |
| Kindle Fire HD 8,9 | Snapdragon 800 | O AVE trava após vários switches ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemas gerais de desempenho com o AVE em vez do AIR. Áudio/vídeo fora de sincronia, a reprodução de vídeo congela após a reprodução entre 9 e 15 minutos. Travamentos. | Possivelmente relacionado ao openGLES que ativamos no AIR. Sob investigação. |  |
| Nexus 7 (2ª geração) | S4Pro APQ8064 (Qualcomm) | O dispositivo trava quando um filme é pausado por mais de 30 minutos. | Problema de dispositivo relatado ao Google. | O aplicativo deve expirar para não permitir um estado de pausa longa. |
| Nexus S (GB) | Humming Bird | Não é possível reproduzir nenhum vídeo usando o decodificador de hardware. | Não há decodificador de HW baseado em Stagefright no Nexus S, então para Android 2.3 estamos usando um decodificador de SW. | Atualize para o ICS. |
| Nexus S (ICS) | Humming Bird | O vídeo ocasionalmente pisca. | Dados incorretos podem fazer com que o decodificador entre em um estado incorreto. | Reinicie o dispositivo. |
| Nook tablet Android OS: 2.3 | TI OMAP 4 | O vídeo não é reproduzido e o aplicativo trava. | O Stagefright entra em um estado instável após executar o aplicativo por algumas vezes. As chamadas para mediaplayer::QueryCodecs travam. | Reinicie o dispositivo para redefinir o estado. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Não é possível instalar o aplicativo SampleMediaPlayer. | Usa o ARM v6 em vez do chipset mais comum do ARM v7. FP/AIR não oferece suporte a este dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | Não é possível reproduzir o vídeo. | Este chipset é um decodificador desconhecido para Android pre-ICS no AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | O desempenho de vídeo não é equivalente a este dispositivo. | O decodificador de hardware está retornando quadros decodificados com o PTS errado. Parece que o decodificador está usando o tempo de decodificação em vez do tempo de apresentação. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI OMAP4 | Falha ao iniciar o vídeo. |  | Atualize para o Android 2.3.7 ou 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | Intermitentemente, o vídeo congela e somente o áudio é reproduzido, depois fica sem resposta. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | O vídeo congela. | Investigando. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | A transição do MBR pode levar até três segundos. | Como uma correção para falhas de MBR, reiniciamos o decodificador para cada switch de fluxo, que pode levar até três segundos. |  |
| Samsung Galaxy Y |  | Não é possível instalar o aplicativo SampleMediaPlayer. | Usa o ARM v6 em vez do chipset mais comum do ARM v7. FP/AIR não oferece suporte a este dispositivo. |  |
| Xoom | Tegra | Alguns quadros são descartados para switching. O decodificador não foi reiniciado. | Limitação OMXAL. |  |

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
