---
title: Notas de versão do TVSDK 1.4 para Android
description: TVSDK 1.4 para Notas de versão do Android descreve o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---


# TVSDK 1.4 para Notas de versão do Android {#tvsdk-for-android-release-notes}

TVSDK 1.4 para Notas de versão do Android descreve o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 1.4.

## Novos recursos {#new-features}

**Versão 1.4.43**

**Carregamento de anúncio seguro por HTTPS**

A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios do Primetime e o CRS por HTTPS.

**alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando esse parâmetro for definido, use a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

Ele aceita um valor de parâmetros booleanos. Se seu valor for `True`, o cliente usará a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

**Versão 1.4.42**

**Inserção parcial de ad-break:**
experiência semelhante à da TV de participar do meio de um anúncio sem acionar o rastreamento do anúncio parcialmente assistido.
Exemplo: O usuário junta-se ao meio (em 40 segundos) de um ad break de 90 segundos que consiste em três anúncios de 30 segundos. Isso é de 10 segundos no segundo anúncio no intervalo.
* O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido do terceiro anúncio.
* Os rastreadores de anúncios do anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores somente do terceiro anúncio são disparados.

**Versão 1.4.41**

Nenhum recurso novo.

**Versão 1.4.40**

Nenhum recurso novo.

>[!NOTE]
>
>Você não precisará das alterações da API se tiver uma versão anterior à 1.4.39.

**Versão 1.4.39**

* O TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.
* O Android TVSDK foi atualizado para fazer solicitações de CRS do novo host do Akamai `primetime-a.akamaihd.net`.
* A nova configuração de nome de host fornece a entrega de ativos CRS por HTTP e HTTPS (SSL) em maior escala.
* O TVSDK suporta a versão Android Oreo.
* Uma nova função é adicionada à classe `AdClientFactory` para suportar o registro de vários Detectores de Oportunidades:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Isso deve retornar uma matriz de PlacementOpportunityDetector. Agora você pode registrar vários Detectores de oportunidades. Por exemplo, para o recurso de saída de anúncio antecipado, eram necessários dois Detectores de oportunidade: um para a inserção do anúncio e outro para a saída antecipada do anúncio. Você só precisará implementar essa nova função se tiver implementado seu próprio AdvertisingFactory (e não usar DefaultAdvertisingfatory). Para obter o comportamento existente, você precisa criar um único Detector de Oportunidade, como na função createOpportunityDetector() , colocar em uma matriz e retornar:

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
>Você não precisará das alterações da API se tiver uma versão anterior à 1.4.39.

**Versão 1.4.36**

Correção de erros para Conteúdo ignorado no Android.

**Versão 1.4.35**

* **Informações de anúncio de rede**

   As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. ID do anúncio, Sistema de anúncio e Extensões de anúncio VAST são fornecidas na classe NetworkAdInfo acessível por meio da propriedade networkAdInfo em um Ad Asset. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como **Moat Analytics**.

**Versão 1.4.31**

**Suporte a várias CDN para anúncios CRS**
* Por padrão, todos os ativos transcodificados serão hospedados na CDN Adobe no Akamai. Com a versão mais recente, o Adobe Creative Repackaging Service (CRS) fornece a capacidade de fazer upload dos anúncios transcodificados em várias CDNs, conforme especificado pelo cliente.
* Novas APIs são adicionadas ao TVSDK para permitir a especificação do url criativo do CRS final quando o url padrão não é usado. Consulte a documentação para saber como usar essas novas APIs.

**A versão 1.4.18**
O Primetime Android TVSDK agora é compatível com as criações de Javascript VPAID 2.0 para permitir uma rica experiência interativa de anúncios em fluxo. Para obter mais informações sobre o VPAID 2.0, consulte [VPAID ad support](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versão 1.4.17**

O AC-3 5.1 é compatível somente com o Amazon FireTV.

**Versão 1.4.11**

* **Ad Fallback, Daisy chaining in ad selection logic (Zendesk #3103** Para anúncios VAST (criações) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Ad fallback for VAST and VMAP ads](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Biblioteca do Video Heartbeats (VHL) atualizada para a versão 1.5**
   * Capacidade de enviar metadados com início de vídeo e/ou início de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - Os heartbeats têm menos em média e menor tamanho

**Versão 1.4.7**

* **Suporte para individualização no local** para instalações no local do servidor de individualização do Adobe para personalizar a solicitação de individualização do cliente para ir para um terminal diferente.

**Versão 1.4.6**

* **Criptografia AES de amostra (requer o Flash Player versão 17.0.0.134)**A criptografia AES baseada em amostra agora é suportada.

**Versão 1.4.2**

* **Atualização da Biblioteca do Video Heartbeats (VHL) para a versão 1.4.0.1**

   * Adicionada a capacidade de agrupar diferentes casos de uso de análises, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete . O ad break é inferido das chamadas de método trackAdStart e trackAdComplete .
   * A propriedade do indicador de reprodução não é mais necessária ao rastrear anúncios.

* **** Integração de SDK da NielsenO TVSDK agora oferece suporte ao envio de informações de rastreamento de usuário para o SDK da Nielsen sem qualquer integração personalizada.

**Versão 1.4.0**

* **Sinalização de blecaute com** substituição de conteúdo alternativoComo parte da atualização do TVSDK 1.4, o TVSDK agora também oferece suporte para entrar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos de manifesto em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remover/substituir** anúncios C3Agora, nenhum trabalho de preparação adicional é necessário para inserir dinamicamente novos anúncios em ativos de VOD (video-on-demand) que estão saindo da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova funcionalidade poderosa também é útil nos casos em que o conteúdo ao vivo/linear é transmitido durante a transmissão e é imediatamente suspenso para uso como conteúdo sob demanda, sem tempo adequado para &quot;limpar&quot; o ativo.

* A interface PlaybackEventListener tem um novo método chamado onReplaceMediaPlayerItem, que pode ser usado para acompanhar um novo evento, `ITEM_REPLACED`. Esse evento é enviado sempre que uma instância MediaPlayer item é substituída no MediaPlayer. O aplicativo cliente que implementa este PlaybackEventListener deve implementar ou substituir esse novo método.
* AdClientFactory tem uma nova função adicionada à classe para registrar para vários Detectores de Oportunidades:

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

* A interface PlaybackEventListener tem um novo método chamado onReplaceMediaPlayerItem, que pode ser usado para acompanhar um novo evento, ITEM_REPLACED. Esse evento é enviado sempre que uma instância MediaPlayer item é substituída no MediaPlayer. O aplicativo cliente que implementa este PlaybackEventListener deve implementar ou substituir esse novo método.

* AdClientFactory tem uma nova função adicionada à classe para registrar para vários Detectores de Oportunidades:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Por exemplo, para o recurso de saída de anúncio antecipado, você precisa de dois Detectores de oportunidades: um para a inserção do anúncio e outro para a saída antecipada do anúncio.

Para substituir essa nova função, crie um único Detector de oportunidades, coloque-o em uma matriz e retorne:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Certificação e suporte do dispositivo no 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Os seguintes recursos são **não** compatíveis com o TVSDK :
>
>* Movimentação lenta em qualquer plataforma ou versão.
>* Brincadeira ao vivo.


**Versão 1.4.43**

O TVSDK 1.4.43 foi certificado com dispositivos Android com Android 6.0.1/ 7.0 e 8.1 (Oreo).

* **Versão 1.4.23:**

   * O TVSDK 1.4.23 foi certificado para dispositivos Android com Android N.

* **Versão 1.4.18:**

   * O Primetime foi certificado para Amazon Fire TV.
   * O VPAID 2.0 é compatível somente com dispositivos com Android 4.0 e superior.

## Problemas resolvidos em 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Todos os clientes TVSDK que usam CRS são altamente incentivados a atualizar para TVSDK 1.4.39 ou posterior no iOS e Android. Essa atualização é uma substituição direta da implementação do aplicativo existente. Após a atualização, verifique as solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo, Charles) para verificar se a versão no caminho reflete a versão 3.1. Por exemplo:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versão 1.4.43**

* Tíquete nº 27143 - Não é possível reproduzir a faixa de áudio 5.1 em dispositivos FireTV

   * O TVSDK agora pode reproduzir áudio AC3 em dispositivos FireTV. A reprodução está sempre em estéreo.

* Tíquete #33902 - Entrega de anúncio seguro por HTTPS

   * A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios do Primetime e o CRS por https.

* Bilhete nº 34493 - Atraso de áudio Bluetooth

   * Adição de `alwaysUseAudioOutputLatency` na classe MediaPlayer, que quando definida, resultará no uso da latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

* Tíquete #34949 - Nova versão da biblioteca de pulsação de vídeo (VHL) integrada.

**Versão 1.4.42 (1791)**

* Zendesk nº 33719: A Taxa de bits adaptável FireTV 4k é dimensionada lentamente. Adição de suporte para ABR para dispositivos FireTV 4K.
* Zendesk nº 33338:  resetDRM limpa todos os dados do aplicativo.  Casos extras tratados em que as exceções em threads que não são TVSDK faziam com que as filas de operação do TVSDK fossem preenchidas.

**Versão 1.4.41 (1776)**

* Zendesk #33002 - Dados de ativos complementares do TVSDK no Fire TV. Implementação de uma nova classe AdBannerAsset que retornará os dados complementares como List &lt;AdBannerAsset> e AdAsset::id agora é uma String em vez de longa.
* Zendesk #32821 - O reprodutor Android Primetime congela ao encontrar o PTS (Presentation Timestamp, carimbo de data e hora de apresentação) para WWE. Esse problema é corrigido nesta versão.
* Zendesk #33572 - VideoAnalyticsProvider Ad Start Crash. Usar a combinação correta da versão SDK conjunta VHL+Nielsen do VideoHeartbeat.jar corrigiu esse problema.
* Zendesk # 33355 - Fire TV: Limpe 15 segundos. Nenhuma correção do TVSDK e do cliente está verificando isso no End e em terceiros.

**Versão 1.4.40 (1764)**

* Zendesk # 33068 - Problema de sincronização de lábios do Amazon no novo dispositivo. O problema de sincronização de lápis é corrigido nestas versões.
* Zendesk #32215 - Android TVSDK 1.4.38 Problemas de segurança `[Hotlist]`. Atualizado para o OpenSSL-1.1.0 e o curl-7.5.1 mais recentes.
* Zendesk #32920 - Tela em branco em uma quebra de anúncio e sem conclusão de quebra de anúncio. Correção de um problema em que um contêiner VPAID poderia entrar em um estado suspenso e lidar com um problema em que os anúncios VPAID do Facebook costumavam retornar vários blocos CDATA em um único \&amp;lt;AdParameters\&amp;gt; nó VAST.

**Versão 1.4.39 (1744)**

* Zendesk nº 28976 - A solicitação de licenciamento demora mais de um segundo. Enquanto as chamadas de solicitação de licença de DRM que usam POST são executadas, Curl adiciona &quot;Expectativa: 100-continue&quot;. Remoção do cabeçalho &quot;Expect:&quot; em TVSDK .
* Zendesk #27707 - Ambientes CSAI que não respeitam os marcadores CUE IN para retorno antecipado ou retorno ao conteúdo. Suporte fornecido para geradores de oportunidade múltipla.

**Versão 1.4.38 (1722)**

* Zendesk nº 21590 - Desempenho e rastreamento de vídeo nas criações de origem mais recentes

Integração e certificação do VHL 2.0 no TVSDK para reduzir a barreira na implementação da VideoHeartbeatsLibrary ao diminuir a complexidade das APIs.

* Zendesk #29688 - Suporte para clientes Android O Beta.

Suporte TVSDK para a nova versão do Android Beta.

**Versão 1.4.36 (1713)**

* Zendesk #27392 - Conteúdo ignorado no Android

Para acomodar a descriptografia, o Android TVSDK estava ampliando incorretamente o intervalo de bytes do conteúdo não-iframe em 16 bytes. O alargamento é necessário para fluxos de Iframe, mas não para fluxos que não sejam de iframe.

**Versão 1.4.34 (1702)**

* Zendesk #27638 - Vazamento no objeto cURL INet

O objeto Posix cURL INet vazava ao manter o gerenciador de compartilhamento e o cache DNS usados nas conexões cURL.

Esse problema foi resolvido excluindo o objeto do URL do Posix INet do desconstrutor do INet.

**Versão 1.4.33 (1694)**

* **Biblioteca OpenSSL**

A biblioteca OpenSSL foi atualizada com o OpenSSL versão 1.0.2j.

* Zendesk #21701 - Envia o URL criativo original para solicitação de CRS 1401 em vez do URL normalizado.
Esse problema é resolvido enviando os URLs criativos originais.

* Zendesk #25023 - Reprodução de vídeo de longa duração: congelamento de vídeo, cintilação de tela
Esse problema foi resolvido definindo as dimensões máximas do formato de vídeo para os dispositivos set-top box CenturyLink.

* Zendesk #27460 - A nova conta Akamai não consegue lidar com uma solicitação de cdn do POST.
O código foi atualizado para fazer com que a solicitação do anúncio `cdn.auditude.com` seja GET em vez de POST.

* Zendesk #28245 - O estado da reprodução não é notificado corretamente quando o aplicativo vai do segundo ao primeiro plano
Esse problema foi resolvido restaurando corretamente o estado de reprodução para reproduzir ou pausar quando o aplicativo retorna ao primeiro plano.

**Versão 1.4.32 (1682)**

* Zendesk #25779 - Vulnerabilidade de segurança encontrada com TVSDK
O Android 4.2 e anterior apresenta uma vulnerabilidade de segurança quando o JavaScript está ativado em um WebView. O uso do WebView por TVSDK foi desativado para dispositivos que estão executando o OS 4.2 ou anterior. Isso desativa o uso de anúncios VPAID em TVSDK nesses dispositivos.

* Zendesk # 26890 - Problema no estado da TELA (ATIVADO/DESATIVADO) que manipula o Ref. Player
Quando o mecanismo de vídeo Adobe (AVE) retorna de um estado SUSPENSO, o DefaultMediaPlayer não atualiza seu status. Como resultado, o DefaultMediaPlayer permanece em um estado SUSPENSO, mesmo que o AVE esteja em um estado REPRODUZINDO. Esse problema foi resolvido definindo o estado DefaultMediaPlayer como PLAYING ao receber um status PLAY do AVE, mesmo que o status atual do DefaultMediaPlayer seja SUSPENSO.

**Versão 1.4.31 (1675)**

* Zendesk #21974 - Exceções devido a objetos nulos
   * AdIndex raramente é incrementado quando nulo. Isso pode ser devido a chamadas de API incorretas recebidas para adBreak precedente. Correção dos tipos de dados para evitar essas exceções

* Zendesk #24714 - Desativar registro irrelevante
   * Atualização do TVSDK para desativar o registro em log de erros

* Zendesk #24488 - AV Sync issues on Fire TV
   * Corrigido melhorando a manipulação dos encadeamentos do decodificador de AV. Especificamente, sempre que as filas de quadro de entrada ou saída são modificadas, o thread do decodificador específico para o tipo de conteúdo do quadro é executado.

* Zendesk nº 26551 - Corrigir as falhas do CRS
   * Quando a solicitação é HEAD (http head), não precisamos ler o conteúdo porque ele está vazio. Embora seja ok tentar lê-lo, o Android antigo (4.0.x) trava enquanto chamamos read() e o Android mais recente retorna o valor correto (-1) quando chamamos read(). Com base nisso, o código foi alterado para não ler o conteúdo para &quot;head&quot;

* Zendesk #26696 Null Pointer Exception ao acessar TrickPlayManager
   * Corrigido verificando se o objeto TrickPlayManager não é nulo antes de usá-lo.

**Versão 1.4.30 (1659)**

* Zendesk #22675 A duração do ativo não é atualizada para fluxos Live/Lineares
Esse problema foi resolvido fornecendo uma nova API, assetDuration, em PTVideoAnalyticsTrackingMetadata que fornece a duração do ativo para fluxos Live e Lineares.

* Zendesk #25853 Vazamento de memória no TVSDK ao alternar canais
O problema em que um buffer de leitura de arquivo vaza quando o MediaPlayer é redefinido ou liberado durante o download de um arquivo foi resolvido.

**Versão 1.4.29 (1653)**

* Zendesk #21200 - O reprodutor não recupera do estado suspenso quando o aplicativo estava em segundo plano
Quando o reprodutor foi suspenso depois que a troca de fluxo foi sinalizada, a resolução permite que o reprodutor execute a troca de fluxo ao restaurar o reprodutor do estado de suspensão, em vez de restaurar para a posição anterior.

* Zendesk nº 23412 - O reprodutor está preso a uma caixa preta se você clicar em qualquer anúncio nos últimos 3s do ad break
Esse problema é o mesmo do Zendesk nº 21200.

* Zendesk #23616 - Skipped ad break procura muito no futuro
Dependendo do tipo de inserção de anúncio (inserir/substituir), o TVSDK determina se a duração do anúncio é usada no cálculo para determinar o ponto final do ad break.

* Zendesk nº 25078 - Vazamento de memória DRM TVSDK no Android TV STB
O vazamento de memória do objeto do adaptador DRM foi localizado e corrigido.

* Zendesk nº 25067 - Falha na linha do tempo do mecanismo de vídeo
Isso ocorre porque os objetos não foram limpos corretamente e os eventos foram chamados depois que os objetos foram destruídos. O problema foi resolvido adicionando verificações para evitar exceções nulas.

* Zendesk #25352 - Definir cabeçalho HTTP personalizado
Esse problema foi resolvido adicionando um novo cabeçalho personalizado à lista de permissões no TVSDK.

* Zendesk #25617 - Substituição de PTS ao vivo, causando descontinuidade do reprodutor e falha de memória
Esse problema foi resolvido adicionando uma manipulação de sobreposição de PTS no FragmentationHTTPStreamer quando uma sobreposição ocorre no meio de um segmento.

**Versão 1.4.28 (1637)**

* Zendesk #23618 - Ad break events são acionados antes que a política de anúncios seja consultada
Esse problema foi resolvido ao não acionar os eventos AD_BREAK_START e AD_START quando o anúncio é ignorado por causa do perdão. Em vez disso, o evento AD_BREAK_SKIPPED é enviado.

**Versão 1.4.27 (1631)**

* Zendesk nº 23174 - Problema de desempenho ao redimensionar o vídeo
Esse problema foi resolvido provando uma nova API, MediaPlayerView.setSurfaceFixedSize, que permite que o TVSDK acesse SurfaceHolder.setFixedSize() de MediaPlayerView.

* Zendesk #24450 - TVSDK faz solicitações de anúncios duplicadas
Esse problema ocorria quando o tempo decorrido era convertido em longo e não duplo, e esse problema foi corrigido.

**Versão 1.4.26 (1627)**

* Zendesk #21436 - Atualização da biblioteca OpenSSL para a versão 1.0.2h Atualizado a biblioteca OpenSSL para OpenSSL versão 1.0.2h
* Zendesk #23825 - Os cookies não estão sendo incluídos nos retornos de chamada corrigidos por fornecer suporte a cookies do android.

**Versão 1.4.25 (1620)**

* Zendesk #22900 - O fluxo de DRM do Live Adobe Primetime não está sendo reproduzido no reprodutor de referência Android
O problema de alocação de memória foi corrigido.
* Zendesk #23176 - O aplicativo falha ao tentar reproduzir anúncios VPAID
A falha ocorreu porque o aplicativo não cria uma visualização de anúncio personalizada para renderizar um anúncio VPAID. Esse problema foi resolvido ao ignorar os anúncios VPAID na resposta do servidor de publicidade quando não há visualização de anúncio personalizada.

* Zendesk #23153 - SampleAES DRM Stream - Playback stalling in the TVSDK Reference Player
Esse problema é o mesmo do Zendesk nº 22900.

**Versão 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Acionamento de conclusões de conteúdo para transições de vídeo ao vivo
Esse problema foi resolvido com a adição de uma API (trackVideoComplete) para acionar manualmente a conclusão de conteúdo durante uma sessão de rastreamento de vídeo ao vivo/linear.

* Zendesk # 21977 VideoEngineTimeline Crash durante a operação placeAdBreak/acceptAd
   * Nesta edição, as seguintes bibliotecas foram atualizadas:
      * Biblioteca do AdobeMobile para a versão 4.10.0
      * Biblioteca do VHL para a versão 1.5.6
      * Biblioteca VHL-Nielsen para a versão 1.6.7

Esse problema foi resolvido adicionando uma verificação nula antes de adicionar anúncios à lista de anúncios aceitos.

* Zendesk #22313 A taxa de bits das STBs com chipset Amilógico não vai além de 1,2 M
Esse problema foi resolvido com o pré-carregamento dos recursos do codec de mídia e a desativação do switch contínuo para dispositivos de chipset Amilógico.

* Zendesk #19520 AES AES HLS de amostra não reproduzindo em players TVSDK
Esse problema foi resolvido com o manuseio de vários descritores PMT para fluxos HLS criptografados por AES de amostra.

**Versão 1.4.23 (1602)**

* Zendesk #18852 - Atualizar lógica de seleção criativa com base nas regras do CRS
Esse problema foi resolvido adicionando um arquivo de configuração JSON para especificar a prioridade da seleção criativa.

* Zendesk #20861 - Android N
Esta versão oferece suporte para Android N, removendo a capacidade de usar diretamente as bibliotecas nativas da plataforma Android que não estão mais acessíveis para aplicativos executados no Android N.

* Zendesk #21018 - Android N crash
Mesma resolução que ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter falha em um erro Invalid_Key
O erro Invalid_Key não inclui uma descrição do AVE, portanto, analisar o texto resultou em NPE. O problema foi resolvido adicionando uma verificação nula para a descrição durante o onError antes de analisar a descrição.

* Zendesk nº 22286 - A biblioteca nativa está alocando a chave/fragmento de leitura da memória causando falhas
Essa falha que ocorria no Android ao tentar carregar um manifesto com várias chaves simultaneamente foi corrigida.

**Versão 1.4.22 (1581)**

* Zendesk nº 17236 - Tempo de reprodução não confiável para vídeos HLS com DRM
O salto de tempo com os fluxos LBA, onde a hora de início do segmento de áudio não corresponde à hora de início do segmento de vídeo, foi corrigido.

* Zendesk #17680 - A reprodução de vídeo está congelando na caixa Selevision Andredo
O decodificador de vídeo nesse dispositivo às vezes retorna um salto de tempo de saída significativo ao colocar o quadro de vídeo na fila do buffer de saída, e esse carimbo de data e hora de saída permanece alto. Esse problema foi resolvido retornando um erro *video profile not supported* que não força o reprodutor a tentar novamente o mesmo perfil ou a escolher um perfil diferente.

* Zendesk nº 19074 - Congelamento de vídeo durante reprodução de truques de FFWD e REW
Esse problema foi resolvido adicionando um novo aviso TRICKPLAY_ENDED_DUE_TO_ERROR para notificar ao aplicativo que a trickplay saiu e que o vídeo foi pausado devido a um erro irrecuperável.

* Zendesk #19574 - TVSDK não retorna dados de resposta M3U8 para conteúdo de DRM ou não-DRM
Esse problema foi resolvido das seguintes maneiras:

* Zendesk #19986 - Comportamento de OP quebrado para certos dispositivos como Android TV
* Adicionando um erro FILE_NOT_FOUND à condição.
* Quando o erro vem de um erro *file not found*, separando o URL e a resposta da descrição do erro se a resposta estiver disponível.
O erro lógico que foi introduzido pelo suporte ao operador do escudo NVidia foi corrigido. Em dispositivos blindados não NVidia, confie nos sinalizadores seguros de exibição mesmo quando o tipo de exibição for desconhecido.

* Zendesk #20549 - Manuseio de listas de reprodução obsoletas. Esse problema foi resolvido reduzindo o intervalo entre a atualização do manifesto ao vivo para metade da duração do segmento esperada, se a busca anterior não receber novos segmentos.

* Zendesk #20742 - O uso de memória parece continuar aumentando ao reproduzir conteúdo ao vivo no FireTV. A falha é causada pela tabela de referência de objeto JNI que atingiu o limite. Esse problema foi resolvido excluindo a referência ao objeto MediaFormat criado durante a reinicialização do decodificador.

* Zendesk #21125 - Retorne do live/linear ad break precocemente (CSAI). Adição de um recurso que permite que o reprodutor retorne ao conteúdo principal durante um ad break, caso o reprodutor registre a divisão em dicas de anúncio usando o splice no detector de oportunidade.

* Zendesk #21334 - Valor de tempo limite da solicitação de anúncio TVSDK para solicitação de anúncio de terceiros. Uma configuração adRequestTimeout foi adicionada a AdvertisingMetadata que permite um tempo limite global para a chamada de anúncio.

**Versão 1.4.21 (1566)**

* Zendesk #17781 - A captura de tela do ADB não funciona mais
Esse problema foi resolvido adicionando a API DefaultMediaPlayer.create (Context context, boolean secureSurface), que permite captura de tela.
Para permitir capturas de tela, passe false para secureSurface.
Importante: Recomendamos que você não ative esse recurso de captura de tela em uma configuração de produção.

* Zendesk nº 19074 - Congelamento de vídeo durante reprodução de truques de FFWD e REW
Os seguintes problemas que ocorreram quando o trickPlay podia congelar na reprodução foram resolvidos:

* Zendesk #19532 - Close Caption está aparecendo fora de ordem
   * O FHS inicia o trickplay, mas o primeiro segmento de iframe não tinha um quadro nele.
   * Durante o download de um segmento de iframe, se o FHS atingir uma condição de erro, ele sairá da reprodução do trickplay e pausa a reprodução.
   * A implementação Android MediaCodec aguarda sempre a disponibilidade da fila de entrada enquanto foi solicitado que liberasse todos os buffers de entrada/saída.
Esse problema foi resolvido revertendo a ordem das dicas da WebVTT, de modo que várias dicas de sobreposição pareçam &quot;rolar para cima&quot;.

* Zendesk #19574 - O TVSDK não retorna dados de resposta M3U8 para conteúdo de DRM ou não-DRM
Na carga inicial do arquivo de manifesto em PTMediaPlayerItem.preparationToPlay, se o carregamento falhar, o TVSDK não informa o corpo da resposta de falha ao aplicativo.
Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro para o aplicativo.

* Zendesk #19701 - Congelamento de reprodução com SAP/Descontinuidade
O congelamento do reprodutor quando o áudio e o vídeo estiverem desalinhados em descontinuidade foi resolvido.

* Bug #PTPLAY-11162 - A atualização da biblioteca OpenSSL para a versão 1.0.2f foi resolvida.

**Versão 1.4.20 (1546)**

* Zendesk #17384 - Solicitação de recurso: Suporte a metadados ID3 para reprodução AAC
O suporte para tags ID3 em mídia AAC foi fornecido no TVSDK para Android a partir da versão 1.4.20.

* Zendesk #18358 - O reprodutor congela no switch de taxa de bits com descontinuidades fora de sincronia
Esse problema foi resolvido manipulando adequadamente os casos de borda de costura de ABR.

* Zendesk #19232 - O aplicativo que usa TVSDK 1.4.18 está se comportando estranhamente no Amazon OS versão 4 mais antigo
Esse problema foi resolvido com a remoção da criação de visualização da Web oculta no processo de inicialização do reprodutor TVSDK para evitar conflitos com dispositivos que não oferecem suporte à visualização da Web do Android.

* Zendesk #19585 - Reprodução de movimento lento quando ocorre transição de taxa de bits adaptável.
Durante a troca ABR, se o novo perfil tiver uma taxa de amostra de áudio diferente do perfil atual, a reprodução se tornará rápida ou lenta. Isso ocorre porque o apresentador de vídeo não é notificado de que o formato de áudio foi alterado.
Esse problema foi resolvido verificando se o sinalizador de notificação está definido no local correto.

* Zendesk #19683 - SAP DAI playback - Sem áudio por alguns segundos.
Para vários casos na lógica do TVSDK, quando o carimbo de data e hora de dois segmentos de renderização foi comparado, RENDITION_TIMEOUT_THRESHOLD foi usado como um intervalo de valor aceitável, pois o carimbo de data e hora nem sempre pode ser correspondido com uma diferença de 0 ms. Se a lacuna estiver dentro do intervalo de RENDITION_TIMEOUT_THRESHOLD, a suposição é que é uma correspondência.

O RENDITION_TIMEOUT_THRESHOLD foi definido como 100 ms, mas foi considerado insuficiente para determinados fluxos. Esse problema foi resolvido aumentando o RENDITION_TIMEOUT_THRESHOLD para 200 ms.

* Zendesk #19699 - O TVSDK falha ao alternar entre as faixas de legendas de VTT
Esse problema foi resolvido fazendo o despejo do reprodutor e recarregando o manifesto quando um rastreamento é alterado e corrigindo o problema de conversão da string UTF8 que afetou os nomes de rastreamento da legenda WebVTT de byte duplo.

* Zendesk nº 19717 - Problema de exibição das opções CC
Esse problema foi resolvido manipulando corretamente a cadeia de caracteres Unicode.

* Zendesk #19910 - Tags TIT2 ID3 não detectadas
Esse problema foi resolvido fornecendo suporte mais completo para codificações de sequência de caracteres ID3 v2.4 e para suporte para ID3 v2.3.

* Zendesk #20135 - O TVSDK está acionando vários OnComplete para conteúdo de VOD.
Esse problema foi resolvido adicionando o ouvinte de evento post_roll_complete no local certo, em vez de no caso completo do evento de alteração de status.

**Versão 1.4.19 (1521)**

* Zendesk #4180 - O TVSDK não está aplicando o HDCP.
   * Esta é uma correção parcial para este tíquete e aborda apenas o problema para dispositivos de proteção NVidia.
Você deve usar a API de detecção HDCP implementada corretamente no Nvidia Shield para rastrear dinamicamente o status do HDCP.

* Zendesk #18358 - O TVSDK congela no switch de taxa de bits com descontinuidades fora de sincronia.
   * Esse problema foi resolvido adicionando um novo aviso para detectar a descontinuidade do PTS e forçando a verificação do PTS a refazer a pesquisa pelo segmento correto para cada switch ABR.
Para corrigir o congelamento, a chamada para o método mediaPlayer.setCustomConfiguration deve incluir forcePTSCheckForABR como um argumento.

* Zendesk #19038 - Nenhum stream ao vivo no Asus Zenpad 10.

   Esse problema foi resolvido pré-carregando as informações do codec de mídia, para que você não consulte a função em tempo de execução.

* Os seguintes problemas são os mesmos do Zendesk #19038:
   * Zendesk #19483 - O TVSDK está travando na plataforma Intel.
   * Zendesk #19171 - Travamentos no Asus Memo Pad 7 com Android 5.0.

**Versão 1.4.18 (1503)**

* Zendesk #3324 - Os relatórios de anúncios do Primetime não rastreiam ad breaks quando não há mídia de anúncio em um VMAP.
Quando um ad break está vazio, o início e a conclusão dos eventos de rastreamento do ad break não eram ping. Esse problema foi resolvido enviando pings de início de ad break em ad breaks vazios, como VMAP AdBreak, com um nó AdSource válido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) é ignorado após a chamada MediaPlayer.reset()
Esse problema foi resolvido adicionando setCCVisibility(Visibility.INVISIBLE); à função reset() na classe MediaPlayer.

* Zendesk #18328 - Dropped frame issue on Amazon Fire TV 2nd gen devices for the content with 60FPS (Problema de quedas de quadros em dispositivos de segunda geração da Fire TV do Zendesk nº 18328 - Conteúdo com 60FPS)
Esse problema foi resolvido aplicando o FPS codificado para a tomada de decisão do tempo de espera e com uma lógica de previsão de FPS mais codificada.

**Versão 1.4.17 (1472)**

* Zendesk #2231 - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotification
Esse problema foi resolvido incluindo o corpo da resposta do manifesto quando há um erro de análise.

* Zendesk #17703 - VideoEngineView não impede capturas de tela durante a reprodução do vídeo
O método setSecure está disponível desde a API 17, mas como a API 17 abrange as versões 4.2, 4.2.1 e 4.2.2, não se sabe qual lançará uma exceção ou se é específica do dispositivo. Esse problema foi resolvido vinculando VideoEngineView.setSecure à cláusula try catch.

* Zendesk #17919 - A busca de conteúdo causa erro de pulsação
Um erro de Posição de dados de entrada inválido estava ocorrendo como resultado da chamada de pulsação gerada quando a busca foi iniciada após a exibição prévia. Esse problema foi resolvido.

**1.4.16a**  (1454a)

* Zendesk #18215 - Alguns fluxos AES não conseguem carregar.
Esse problema foi resolvido verificando o tamanho dos metadados do DRM de perfil antes de carregar a chave AES.

**Versão 1.4.16 (1454)**

* Zendesk # 3875 - Tab S Crashes durante a reprodução
Reverter a dependência de OKHTTP no Auditude para CRS porque o TVSDK agora está usando diretamente httpurlconnection em vez de curl. O problema foi resolvido limpando exceções antes de fazer qualquer outra chamada JNI.

* Zendesk nº 4487 - Rastreamento do canal linear de conteúdo
O problema foi resolvido permitindo a reinicialização do rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17919 - Android - A busca de conteúdo causa erro de pulsação
O problema quando a pulsação está em um estado de erro quando há uma busca em um capítulo foi resolvido.

* Zendesk #18053 - Adobe Primetime falha no Marshmallow
O TVSDK estava travando no Android M OS quando a biblioteca TVSDK usava um código neon que faz a conversão de cores YUV -> RGB. O problema foi resolvido atualizando as funções que estão causando esse problema usando a versão que não é neon do código.

* Zendesk #18072 - Android M - Falha do aplicativo
Ao verificar se o perfil e o nível são suportados, ocorre uma falha ao chamar as APIs MediaCodecList e MediaCodecInfo. O problema foi resolvido fornecendo uma solução temporária carregando todas as informações do codec antecipadamente para evitar chamar essas APIs somente quando as informações do codec forem necessárias.

* Zendesk #18074 - Legendas árabes que não funcionam no Nexus com Android 6.0
O problema foi resolvido fornecendo suporte ao mapa de fontes CTS para Android.

**Atualização da versão 1.4.15 (1438)**

* Zendesk #17437 - Atraso longo na inicialização do conteúdo VOD com alguns fluxos AES.
Para resolver esse problema, se várias chaves estiverem listadas no manifesto, baixe todas as chaves AES em paralelo.

**Versão 1.4.15 (1435)**

* Zendesk #4278 - Glitches no Android configuram as caixas superiores quando a taxa de bits adaptável muda (ABR).
A correção foi adicionar suporte para switch ABR perfeito com o codec de mídia Android mais recente.

* Zendesk #17063 - Chamar mediaPlayer.reset() causa um erro de redefinição do mecanismo de vídeo.
A correção era incluir o MediaErrorCode original de VideoEngineExceptions ao despachar ErrorEvents.

* Zendesk #17130 - Uma pausa breve, mas perceptível, ao alterar a taxa de bits vista no FireTV.
(Igual ao número 4278 acima) A correção foi adicionar suporte para switch ABR sem interrupções com o codec de mídia Android mais recente.

* Zendesk # 17666 - Marcadores de anúncios adicionais, Inesperados ou Sem anúncios ao retomar o conteúdo.
A correção foi um problema ao fazer conteúdo prepareToPlay on video-on-demand (VOD), a busca inicial é executada no horário local, em vez do horário virtual.

* Zendesk #17437 - Atraso longo na inicialização do conteúdo VOD com alguns fluxos AES.
A correção foi baixar todas as chaves AES em paralelo quando várias chaves estão listadas no manifesto.

* Zendesk #17851 - Android TV - Quadro Preto durante ABR
A correção foi especificar KEY_MAX_WIDTH e KEY_MAX_HEIGHT para ativar a reprodução adaptável.

**Versão 1.4.14 (1415)**

* Zendesk # 3875 - Tab S Crashes durante a reprodução.
Foi necessária uma correção adicional para evitar a falha.

* Zendesk #17245 - Fallback on Android TV não está funcionando.
Correção de um problema adicional em que a reprodução travava quando o fallback era ativado e a resposta VMAP tinha um ad break vazio.

**Versão 1.4.14 (1412)**

* Zendesk #17245 - Fallback on Android TV não está funcionando.
Remoção de uma restrição para desativar o reempacotamento criativo em anúncios de fallback.

**Versão 1.4.13 (1388)**

* Zendesk nº 3502 - Suporte a failover baseado no cliente HLS durante um ad break
Permitir failover para o manifesto principal ao atualizar o erro de perfil ativo ocorre durante o período de ad break.

* Zendesk # 3875 - Tab S Crashes durante a reprodução
Para resolver o conflito entre HttpUrlConnection e cURLm, use uma biblioteca de terceiros.

* Zendesk #4450 - problema ao configurar metadados personalizados para uma única disposição em um resolvedor de conteúdo
Adicione um setter às configurações de Oportunidade.

**Versão 1.4.12 (1388)**

* Zendesk nº 2751 - CSAI e CRS | Reforçar: Manipule elementos dinâmicos em determinados URLs de arquivo de mídia.
Serviço de reempacotamento criativo atualizado para lidar corretamente com anúncios com URLs criativos dinâmicos.

* Zendesk #3965 - Alternar para a reprodução normal a partir da reprodução de vídeo resulta em um salto para frente um pouco antes de iniciar a reprodução.
   * A correção inclui o TVSDK que retorna o tempo antes da alteração da taxa até que todas as variáveis sejam atualizadas, em vez de tentar calcular o GetStreamTime.
   * Correção de uma falha ao alterar a velocidade da reprodução de truque próxima ao final do fluxo.
   * Cálculo de tempo atual corrigido durante a reprodução de truques.

* Zendesk #3978 - Trickplay às 8x e 16x congela com frequência.
   * Sempre escolha o perfil de reprodução de truque com a menor taxa de bits para evitar buffering constante.
   * Aumente o intervalo do quadro ignorado para obter uma alta taxa de reprodução de truques.
   * Correção de um problema em que o buffer continua crescendo após atingir a duração do target durante a reprodução do truque.

* Zendesk # 3992 - Velocidades adicionais do Trickplay.
O TrickPlay foi atualizado para aceitar taxas superiores a 16x; +/- 32, +/-64 e +/-128 agora também são permitidos.

* Zendesk #4007 - Interpretar o objeto GEOB como parte dos metadados da linha do tempo (Android &amp; Web).
Adição da API setByteArray e getByteArray .

* PTPLAY-7301 - Inicialização instantânea no ponto de acesso aleatório.
O Instant On foi atualizado para permitir um ponto de partida diferente de zero.

**Versão 1.4.11 (1363)**

* Zendesk #2076 - Frequent stutter ao reproduzir vídeo no Motorola Xoom com Android 4.0.3
Adição de dispositivos ao lista de permissões para impedir que eles tentem reproduzir conteúdo de alto perfil.

* Zendesk #2197 - `[Ads]` Rastreamento de erros de anúncio
despache OperationFailedEvent com notificação de aviso.

* Zendesk #3304 - macro VAST 3.0 `[ERRORCODE]` não sendo preenchida
   * o código de erro 400 será exposto se o anúncio em linha apresentar anúncios com conteúdo incorreto.
   * `[ERRORCODE]` macro será codificada no URL

**Versão 1.4.10 (1354)**

* Zendesk #2941 - Os ativos em tempo real não têm &quot;0&quot; no intervalo pesquisável
Anteriormente, havia um buffer de três segmentos ao buscar o início de um fluxo ao vivo, agora é possível buscar o início de um fluxo ao vivo (ou seja, o início do primeiro segmento).

* Zendesk #3169 - Update reference player with Adobe Analytics integrationO reprodutor de referência foi atualizado com a biblioteca Adobe Analytics como exemplo de implantação.
* Zendesk nº 3299 - Comportamento inexplicável de trick play
   * Correção de um erro em que retornar ao estado de reprodução após parar a reprodução de truque poderia levar vários segundos (às vezes mais de 25 segundos).
   * Correção de um erro em que chamar a reprodução de truque uma segunda vez na mesma mídia pode fazer com que o fluxo congele no momento atual.
* Zendesk # 3433 - Android and Flash - Problemas com legendas

GetLine para WebVTT não respeitava um comprimento ajustado &lt;CR>&lt;LF> para um pacote; a última legenda pode conter caracteres de legendas anteriores.

* PTPLAY-6243 - Aprimorar o reprodutor de referência para capturar informações de depuração

Os players de referência de amostra do Android foram aprimorados com uma opção para ativar logs de depuração e enviar os resultados por email. Essa opção é encontrada no menu Log no reprodutor de referência.

**Versão 1.4.9 (1332)**

* Zendesk nº 2649 - Buffer concluído ocorre antes que o buffer inicial esteja cheio

Após uma busca, um possível caso em que o mecanismo de vídeo defina o estado como REPRODUZIR antes que o apresentador de vídeo esteja pronto para a reprodução. Ocorre quando o estado do buffer está alto antes da busca. Correção notificando o mecanismo de vídeo de estado de buffer baixo. Com o mecanismo de vídeo em estado de buffer baixo, chamar Reproduzir causa alteração de estado em BUFFERING, em vez de REPRODUZIR. A reprodução é retomada quando o estado é alterado para PLAYING.

* Zendesk # 2846 - Solicitação de aprimoramento: Fornecer a capacidade de definir diferentes sequências de agente do usuário para chamadas feitas pela biblioteca do Auditude

Uma nova API foi adicionada para definir o agente do usuário para chamadas relacionadas a anúncios, auditudeSettings.setUserAgent(&quot;usuário/agente&quot;). Se nenhum agente de usuário for definido, o padrão será usado. Isso afeta apenas o agente do usuário para chamadas relacionadas a anúncios, o agente do usuário para chamadas de mídia permanece inalterado, que é &quot;Adobe Primetime&quot;+&lt;default useragent>.

**Versão 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Erro com local ... Se o carregamento do manifesto em FragmentateHTTPStreamer::ThreadParseManifest() falhar, verifique se o domínio do URL é localhost e, em caso positivo, altere o domínio para 127.0.0.1 e evite ThreadParseManifest.
* Zendesk #3072 - Mudança automática para taxas de bits mais baixas. Alteração do cálculo do comprimento do buffer para ignorar a carga de PTS zero.
* Zendesk # 3168 - As legendas da WebVTT são exibidas somente durante os primeiros 10 segundos.
* Zendesk #3193 - Solicitação de uma API de alteração de perfil em TVSDK, PlaybackEventListener.onProfileChanged() foi adicionada.

**Versão 1.4.7 (1311)**

* Zendesk # 2197 - Rastreamento de erros de anúncios. A notificação adicionada para o ativo falhou ao carregar o manifesto
* Zendesk nº 2575 - O PSDK ignora o anúncio em fluxo personalizado do MARK antes do vídeo
* Zendesk #2719 - Win Death with auditude ads, rastreamento de beacon corrigido quando redirecionado para url relativo no plug-in auditude
* Zendesk # 2760 - Tag DISCONTINUITY ignorada durante o modo TrickPlay
* Zendesk nº 2805 - Falha do reprodutor no início da reprodução, mesma correção do Zendesk nº 2719
* Zendesk #2817 - Android player - O reprodutor às vezes trava e pára de reproduzir, corrigido ao estender os buffers de decodificação de 2,0 para 3,0 segundos
* Zendesk nº 2839 - O Adobe Primetime PSDK suporta os chipsets ARMv8?, adição de correção para falhas encontradas no Galaxy S6.
* Zendesk #2885 - Auditude Crashing playback, mesma correção que Zendesk #2719
* Zendesk #2895 - Falha ao vivo do HLS consistentemente após 10 minutos de reprodução
* Zendesk #2925 - Feedback about Android dev build (1.4.5), em determinados dispositivos, quando colocamos o pacote na fila de entrada, se o PTS for negativo, o decodificador entrará em um estado estranho que sempre recebemos um PTS de saída negativo para futuros pacotes. A correção definirá o PTS de entrada como zero se for negativo evitar esse problema.
* PTPLAY-4645 - Desative o suporte a cifras RC4 no openssl. Há explosões conhecidas para RC4. Isso significa que, se for feita uma tentativa de conexão com um servidor que suporta apenas RC4, ocorrerá uma falha.

**Versão 1.4.6 (1282)**

* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede precárias, corrigidas pela remoção da implementação rápida do switch.
* Zendesk #2631 - Legendas árabes no Android: O texto em várias linhas aparece recortado, corrigido ajustando o tamanho da fonte para fontes árabes.
* Zendesk #2844 - O tempo de download do buffer na Nota 4 e do Fragmento não é preciso.

Esse problema foi corrigido adicionando latência entre downloads de segmentos de vídeo no cálculo da largura de banda e fazendo com que a lógica de cálculo do tempo de download usasse o tempo de ciclo de solicitação completo.

* Zendesk #2908 - Legendas árabes que não funcionam no Nexust 5, 6 e 7, corrigidas adicionando mais 2 fontes de fallback para scripts árabes.
* PTPLAY-4627 - atualizar o aplicativo Nielson para a versão 1.2.3.7
* PTPLAY-5084 - Suporte a failover de atualização do Manifest ao vivo Principal

**Versão 1.4.5 (1248)**

* Zendesk #1757 - Only audio played or Player crashes for some video bit rate profile, Nexus 4 and Nexus 7 crash fixed
* Zendesk #2072 - TimedMetadata para AdEvent não contém o URL completo apenas &quot;http&quot;
* Zendesk nº 2192 - A taxa de bits nem sempre diminui em condições de rede precárias
* Zendesk #2256 - Access to Principal Playlist, PSDK atualizado para despachar eventos timedMetadata para tags assinadas na lista de reprodução principal.
* Zendesk #2269 - Duas linguagens de legenda diferentes aparecem na tela ao mesmo tempo com a WebVTT
* Zendesk #2417 - Player try tentar baixar legendas antes do início da reprodução, WebVTT estava usando a variável de número de segmento errada para correspondência de números de segmento. Bug só seria exibido para mídia com índices de segmento a partir de zero.
* Zendesk #2470 - PSDK não retorna do estado SUSPENDER quando a alteração na taxa de bits ocorre após a suspensão. Em uma situação especial, quando a busca inteligente é chamada por RestoreGPUResource (o reprodutor de restauração do estado de suspensão) e o switch de fluxo é detectado antes disso, a busca inteligente não pode ser concluída e resultar em buffering constante.
* Zendesk #2451 - Closed captioning &#39;bottom inset&#39;, adição do parâmetro &#39;bottomInset&#39; ao código de legenda
* Zendesk #2480 - desabilitando a otimização de redirecionamento HTTP 302, Adição de suporte para configuração da propriedade useRedirectUrl
* Zendesk nº 2486 - beacons de terceiros
* Zendesk #2547 - Legendas árabes: O texto deve ser alinhado e justificado à direita

**Versão 1.4.4 (1195)**

* Zendesk #1158 - Playback failed on Huawei Valiant (Y301A1)
* Zendesk #1709 - Tamanho de mídia incorreto e vídeo estendido
* Zendesk #1757 - Somente o áudio reproduzido após a troca de perfil entre fluxos com dados spa/pps idênticos
* Zendesk # 2095 - Status HTTP 307 (redirecionamento) faz com que o reprodutor do Adobe pare a reprodução
* Zendesk #2126 - TimedMetaData ausente do último ADEVENT, tags assinadas que existem após o último segmento não foram relatadas ao PSDK do AVE
* Zendesk #2227 - Lockups in VideoEngine nativeReset and nativePause
* Bug #3921755 - Atualização da biblioteca OpenSSL para a versão 1.0.1L

**Versão 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Legenda oculta ativando e desligando
* PTPLAY-1818 - A peça de roteiros de rebobinamento pára no anúncio em vez de rebobinar
* PTPLAY-2736 - Uma legenda WebVTT exibida anteriormente é mostrada na tela quando um fluxo com a legenda WebVTT é concluído na reprodução
* PTPLAY-3773 - Um anúncio intermediário não é reproduzido quando a reprodução do fluxo é iniciada após a posição do anúncio

**Versão 1.4.2**

* Zendesk nº 1561 - Suporte a failover baseado no cliente HLS no primetime. Usará a data do programa para abordar o failover
* Zendesk #1590 - LoadInfo.MediaDuration é sempre 0 (não fixo para somente áudio)
* Zendesk #1626 - Potencial vazamento de memória no Player. Sem vazamento de memória real, o problema foi com o NotificationHistory salvando as últimas 1000 notificações, isso foi reduzido para 100.
* Zendesk nº 2192 - A taxa de bits nem sempre diminui em condições de rede precárias

**Versão 1.4.1 (1121)**

* Zendesk #1951 - Lockup in VideoEngine.nativeReset() on 4.0.x devices
* Zendesk #2064 - Native Crash SIGSEGV em dispositivos Android específicos baseados na intel
* Zendesk #2075 - Lockup in VideoEngine.nativeReleaseGPUResource on 4.0.x devices
Observação: Esta build é ***necessária*** para suporte do Android 5.0 (Lollipop)
* Zendesk #1513 - Suporte do Android Lollipop
* Zendesk #1709 - Tamanho de mídia incorreto e vídeo estendido
* Zendesk #1871 - As legendas da WebVTT desaparecem ocasionalmente e reaparecem ao exibir um livestream com as legendas da WebVTT
* Zendesk #1996 - Nenhum marcador de linha do tempo é visto no PSDK 1.4.0
* Zendesk #2046 - Crash with PSDK 1.4.1.1113, travamento corrigido para fluxos ao vivo quando nenhum anúncio é retornado do auditude
* Bug #3769657 - Atualize a versão do curl para 7.38.0
* PTPLAY-1575 - Quando a reprodução ABR começa com fluxo somente de áudio e depois alterna para fluxo de áudio/vídeo, o vídeo nunca é renderizado enquanto o áudio continua
* PTPLAY-2499 - Atualize para OpenSSL para a versão 1.0.1j para lidar com vulnerabilidades recentes
* PTPLAY-2632 - O vídeo não é recuperado após a conclusão do anúncio intermediário no Android Lollipop
* PTPLAY-2678 - Paralisações de vídeo durante testes de longevidade ao vivo no Android Lollipop

**Versão 1.4.0**

* Zendesk #1024 - Recurso para remover anúncio do fluxo por meio do manifesto
* Zendesk Nº 1293 - Problema De Seleção De Rastreamento De Legendas Fechadas.
* Zendesk #1590 - LoadInfo.MediaDuration é sempre 0, mediaDuration agora mostra o valor correto.
* Zendesk #1629 - reprodutor/aplicativo falha ao terminar a reprodução do anúncio no Galaxy S4
* Zendesk #1674 - ClosedCaption Not displayed, Corrija a exibição da legenda 708 quando os códigos ETX 0x03 estiverem ausentes.
* PTPLAY-2157 - Os estilos de Legendas ocultas padrão foram retornados por getters mesmo se um estilo diferente tiver sido definido e verificado visualmente no stream. As propriedades de estilo de Legenda oculta agora mostrarão o valor para o qual foram definidas.

## Problemas conhecidos no 1.4 {#known-issues-in}

**Versão 1.4.31**

* PTPLAY-16803 - As Legendas ocultas não funcionarão com conteúdo somente de áudio, pois o sistema de legenda precisa de vídeo para funcionar. Sem vídeo, não há dimensão do visor e sem uma dimensão do visor, não é possível exibir gráficos para legendas.
* PTPLAY-1634 - A mesma tag subscrita tem diferentes carimbos de data e hora em diferentes janelas ativas. Quando a janela ativa é movida, a mesma tag deve ter os mesmos carimbos de data e hora. No entanto, às vezes, mesmo tags têm carimbos de data e hora diferentes.
* PTPLAY-3197 - Falha com sinal de erro 11 SIGSEGV no dispositivo Acer Iconia após ~ 1 hora de reprodução contínua
* PTPLAY-3310 - Com um áudio com uma taxa de bits mais baixa, o áudio se torna instável/persistente no Acer Iconia
* PTPLAY-3355 - Falha de MORTE WIN no Motorola Xoom com 4.0.x após ~ 1 hora de reprodução contínua.
* PTPLAY-3557 - O rebentamento em um ad break está fazendo com que o fluxo seja concluído
* PTPLAY-7079 - Janela de reprodução no cliente android não funciona com Secure Stop/Hard Stop
* Bug #3760144 - A resolução pode mudar ou parecer pulsar quando o fluxo é pausado em alguns dispositivos, como Kindle Fire 7 e Samsung Galaxy Nexus. Apenas observável sob controlo estreito
* Bug #3761170 - searchToLocal in Live with Ads não pode buscar novamente conteúdo de anúncio, seu melhor para usar as APIs currentTime para fluxos ao vivo
* Bug #3763370 - Os streams ao vivo com anúncios ocasionalmente mostrarão dois marcadores de anúncio próximos, quando deveria haver apenas um. Esses marcadores de anúncios representam o mesmo anúncio, e apenas um será reproduzido
* Bug #3763373 - O marcador de anúncio pode desaparecer brevemente ao buscar depois de um anúncio em fluxos VOD. O marcador de anúncio é restaurado e não há outro efeito adverso na linha do tempo
* Alguns dispositivos têm problemas conhecidos de reprodução. Consulte [Problemas de dispositivo conhecidos em 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementação de referência - A reprodução de truque não está implementada no aplicativo de amostra
* Em alguns dispositivos Android TV, um quadro preto pode ser visto devido a uma redefinição de decodificador nos seguintes pontos de transição:
   * para dentro e para fora do modo de trickplay
   * alternar entre trilhas de áudio de ligação tardia
   * de um anúncio ao conteúdo principal.

**Versão 1.4.23**

* As Legendas ocultas não funcionarão com conteúdo somente áudio, pois o sistema de legendas precisa de vídeo para funcionar. Sem vídeo, não há dimensão do visor e sem uma dimensão do visor, não é possível exibir gráficos de legendas.
* A partir da versão 1.4.23, o TVSDK não será compatível com o Gingerpão OS 2.3. Isso ocorre porque o TVSDK usou as seguintes bibliotecas privadas do Android para coletar informações de hardware sobre dispositivos com o Gingerpão OS:

   * `libstagefright.so`
   * `libcutils.so`

Na versão Android N, o Google removeu o acesso a essas bibliotecas privadas. O sistema operacional Gingerpão representa atualmente menos de 1% da quota de mercado do sistema operacional Android globalmente, portanto, após a versão 1.4.23, o sistema operacional Gingerpão não será mais suportado pelo TVSDK.
Ao usar a versão 1.4.23 (que inclui suporte para Android N) ou posterior:
* Atualize seus aplicativos para usar a versão 11 do minSdkVersion.
* Se o usuário final estiver executando o OS 2.3, a versão do SDK será menor do que a minSdkVersion do aplicativo. O sistema aborta a instalação ou atualização do aplicativo.
* Se o usuário final estiver executando uma versão superior ao OS 2.3, o aplicativo será instalado corretamente.

Se você atualizar minSdkVersion:

* Se o usuário final estiver executando o OS 2.3, o aplicativo será instalado, mas a reprodução não funcionará.
Isso se aplica à atualização e à instalação atualizada.
* Se o usuário final estiver executando um sistema superior ao OS 2.3, o aplicativo será instalado corretamente e o conteúdo será reproduzido corretamente.

**Versão 1.4.22**

* A saída antecipada dos anúncios não funciona com alguns dos anúncios intermediários quando as tags splice e splice-in estão muito próximas umas das outras.

**Versão 1.4.2**

* O rebobinamento em um ad break está fazendo com que o fluxo seja concluído.

O Media Player envia incorretamente MediaPlayerState.Complete durante a operação de retrocesso de Trick Play, quando ele atinge um limite de anúncio. O reprodutor deve ignorar esse evento quando estiver no modo de reprodução de artifício; caso contrário, o SDK processa o estado corretamente.

**Versão 1.4.0 (1086)**

* PTPLAY-1634 - A mesma tag Subscribed tem diferentes carimbos de data e hora em diferentes janelas ativas. Quando as janelas em tempo real são movidas, a mesma tag em cada uma delas deve ter os mesmos carimbos de data e hora. No entanto, às vezes, mesmo as mesmas tags têm carimbos de data e hora diferentes.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE às vezes é visto após vários switches de/para o fluxo alternativo em blecautes
* Bug #3726865 - Se um fluxo LBA de taxa de bits múltipla iniciar de um fluxo somente de áudio, o vídeo não será exibido se for alternado para um fluxo de áudio/vídeo. Iniciar a partir de um fluxo de áudio/vídeo não exibirá esse problema e poderá alternar com êxito entre fluxos de áudio e áudio/vídeo
* Bug #3760144 - A resolução pode mudar ou parecer pulsar quando um fluxo é pausado em alguns dispositivos, como Kindle Fire 7 e Samsung Galaxy Nexus. Apenas observável sob controlo estreito
* Bug #3761170 - searchToLocal in Live with Ads não pode procurar de volta para o conteúdo do anúncio; é melhor usar as APIs currentTime para fluxos ao vivo
* Bug #3763370 - Os streams ao vivo com anúncios ocasionalmente mostrarão dois marcadores de anúncio próximos, quando deveria haver apenas um. Esses marcadores de anúncios representam o mesmo anúncio, e apenas um será reproduzido
* Bug #3763373 - O marcador de anúncio pode desaparecer brevemente ao buscar depois de um anúncio em fluxos VOD. O marcador de anúncio é restaurado e não há outro efeito adverso na linha do tempo
* Alguns dispositivos têm problemas conhecidos de reprodução. Para obter mais informações, consulte [Problemas de dispositivo conhecidos em 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementação de referência - A reprodução de truque não é implementada no aplicativo de amostra.

## Problemas de dispositivo conhecidos no 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Solução alternativa |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | O Atraso de ABR é esperado, pois está reiniciando o decodificador. |  |  |
| Desejo HTC (diferente do Desejo HTC HD) | QSD8250 | Não é possível reproduzir o vídeo. Retorna o erro VIDEO_PROFILE_NOT_SUPPORTED . | O desejo não fornece um decodificador de hardware adequado. Ele dá o decodificador SW de Stagefright. | Reinicie o dispositivo. |
| HTC EVO 4G | QSD8650 | Não há decodificador de hardware. | O Qualcomm não tem um decodificador de hardware. | Atualize para Android 4.x. |
| Kindle FireSystem versão 6.0 | TI OMAP4 | Não reproduz fluxos HLS. Vídeo no AIR não funciona. |  | Atualize para o sistema versão 6.3. |
| Kindle Fire HD | TI OMAP4 | Pode entrar em um estado em que não pode reproduzir vídeo. Retorna os erros VIDEO_PROFILE_NOT_SUPPORTED e UNRECOVERABLE_ERROR . | O decodificador de hardware entra em um estado irrecuperável quando o aplicativo não encerra totalmente o decodificador de hardware, por exemplo, depois de encontrar uma falha. Também acontece em aplicativos nativos do dispositivo. | Reinicie o dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | A AVE falha após vários switches ABR. |  |  |
| Motorola Atrix | Tapa 2 | Problemas gerais de desempenho com o AVE em vez do AIR. Áudio/vídeo fora de sincronia, a reprodução congela após reproduzir entre 9 e 15 minutos. Falhas. | Possivelmente relacionado a openGLES que ativamos no AIR. A ser investigado. |  |
| Nexus 7 (2ª geração) | S4Pro APQ8064 (Qualcomm) | O dispositivo trava quando um filme é pausado por mais de 30 minutos. | Problema de dispositivo relatado ao Google. | O aplicativo deve expirar para não permitir um estado de pausa longo. |
| Nexus S (GB) | Pássaro Humor | Não é possível reproduzir nenhum vídeo usando o decodificador de hardware. | Não há um decodificador de hardware baseado em Stagefright no Nexus S, portanto, para o Android 2.3, estamos usando um decodificador de SW. | Atualize para ICS. |
| Nexus S (ICS) | Pássaro Humor | Ocasionalmente, o vídeo cintila. | Dados incorretos podem fazer com que o decodificador entre em um estado incorreto. | Reinicie o dispositivo. |
| Tablet de notebookSistema operacional Android: 2,3 | TI OMAP 4 | O vídeo não é reproduzido e o aplicativo trava. | O Stagefright entra em um estado instável após a execução do aplicativo por algumas vezes. Chamadas para mediaplayer::QueryCodecs hang. | Reinicie o dispositivo para redefinir o estado. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Não é possível instalar o aplicativo SampleMediaPlayer. | Usa ARM v6 em vez do chipset ARM v7 mais comum. FP/AIR não suporta este dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | Não é possível reproduzir o vídeo. | Este chipset é um decodificador desconhecido para Android pre-ICS no AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | O desempenho do vídeo não é par para este dispositivo. | O decodificador de hardware está retornando quadros decodificados com o PTS errado. Parece que o decodificador está usando o tempo de decodificação em vez do tempo de apresentação. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI OMAP4 | Falha ao iniciar o vídeo. |  | Atualize para Android 2.3.7 ou 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | Intermitentemente, o vídeo congela e somente as reproduções de áudio, tornando-se sem resposta. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | O vídeo congela. | Investigando. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | A transição de MBR pode levar até três segundos. | Como uma correção para falhas de MBR, reiniciamos o decodificador para cada switch de fluxo, que pode levar até três segundos. |  |
| Samsung Galaxy Y |  | Não é possível instalar o aplicativo SampleMediaPlayer. | Usa ARM v6 em vez do chipset ARM v7 mais comum. FP/AIR não suporta este dispositivo. |  |
| Xoom | Tegra | Alguns quadros são soltos para alternância. O decodificador não é reiniciado. | Limitação OMXAL. |  |

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
