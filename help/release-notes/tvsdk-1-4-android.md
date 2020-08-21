---
title: Notas de versão do TVSDK 1.4 para Android
seo-title: Notas de versão do TVSDK 1.4 para Android
description: As Notas de versão do TVSDK 1.4 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 1.4.
seo-description: As Notas de versão do TVSDK 1.4 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 1.4.
uuid: 8bd8ee42-7a1b-4c14-aad9-22804743e505
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: f1ebc1a8-185a-493a-9c00-a6102dffb128
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '7830'
ht-degree: 0%

---


# Notas de versão do TVSDK 1.4 para Android {#tvsdk-for-android-release-notes}

As Notas de versão do TVSDK 1.4 para Android descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos e os problemas do dispositivo no TVSDK Android 1.4.

## Novos recursos {#new-features}

**Versão 1.4.43**

**Carregamento seguro de anúncios em HTTPS**

A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios primetime e CRS em HTTPS.

**alwaysUseAudioOutputLatency(boolean val) na classe MediaPlayer**

Quando esse parâmetro for definido, use a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

Ele aceita um valor de parâmetros booleanos. Se seu valor for `True`, o cliente usará a latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

**Versão 1.4.42**

**Inserção parcial de quebra de anúncio:**
Experiência semelhante à da TV de participar do meio de um anúncio sem acionar o rastreamento do anúncio assistido parcialmente.
Exemplo: O usuário ingressa no meio (em 40 segundos) de um intervalo de anúncios de 90 segundos que consiste em três anúncios de 30 segundos. Dez segundos depois do segundo anúncio no intervalo.
* O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.
* Os rastreadores de anúncios para o anúncio parcial reproduzido (segundo anúncio) não são acionados. Os rastreadores apenas do terceiro anúncio são disparados.

**Versão 1.4.41**

Nenhum recurso novo.

**Versão 1.4.40**

Nenhum recurso novo.

>[!NOTE]
>
>Você não precisará das alterações da API se estiver em uma versão anterior à 1.4.39.

**Versão 1.4.39**

* O TVSDK é certificado com VHL 2.0.1 e com VHL 2.0.1 com Nielsen.
* O Android TVSDK é atualizado para fazer solicitações de CRS do novo host do Akamai `primetime-a.akamaihd.net`.
* A nova configuração de nome de host fornece delivery de ativo CRS por HTTP e HTTPS (SSL) em maior escala.
* O TVSDK suporta a versão Android Oreo.
* Uma nova função é adicionada à `AdClientFactory` classe para suportar o registro de vários Detectores de Oportunidade:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Isso deve retornar uma matriz de PlacementOpportunityDetector. Agora você pode registrar vários Detectores de oportunidade. Por exemplo, para o recurso de saída de anúncio inicial, eram necessários dois Detectores de oportunidade: um para inserção de anúncio e outro para saída antecipada do anúncio. Você só deverá implementar essa nova função se tiver implementado sua própria AdvertisingFactory (e não usar DefaultAdvertisingfatory). Para obter o comportamento existente - você precisa criar um único Detector de oportunidade, como na função createOpportunityDetector(), colocar em uma matriz e retornar:

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
>Você não precisará das alterações da API se estiver em uma versão anterior à 1.4.39.

**Versão 1.4.36**

Correção de erros para Ignorar conteúdo no Android.

**Versão 1.4.35**

* **Informações sobre anúncios de rede**

   As APIs TVSDK agora fornecem informações adicionais sobre respostas VAST de terceiros. A ID do anúncio, o sistema de anúncios e as extensões de anúncio VAST são fornecidos na classe NetworkAdInfo acessível por meio da propriedade networkAdInfo em um Ad Asset. Essas informações podem ser usadas para integração com outras plataformas do Ad Analytics, como o **Moat Analytics**.

**Versão 1.4.31**

**Suporte a vários CDN para anúncios de CRS**
* Por padrão, todos os ativos transcodificados serão hospedados no CDN de propriedade do Adobe no Akamai. Com a versão mais recente, o Adobe Creative Repacking Service (CRS) fornece a capacidade de carregar os criativos transcodificados em vários CDNs, conforme especificado pelo cliente.
* Novas APIs são adicionadas ao TVSDK para permitir a especificação do url criativo do CRS final quando o url padrão não é usado. Consulte a documentação para saber como usar essas novas APIs.

**A versão 1.4.18** Primetime Android TVSDK agora é compatível com as criações do Javascript VPAID 2.0 para permitir uma experiência avançada de anúncios interativos em fluxo. Para obter mais informações sobre o VPAID 2.0, consulte Suporte [a anúncios](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md)VPAID.

**Versão 1.4.17**

AC-3 5.1 é compatível apenas com Amazon FireTV.

**Versão 1.4.11**

* **Ad Fallback, Encadeamento de margaridas na lógica de seleção de anúncio (Zendesk #3103** Para anúncios VAST (criativos) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo MIME inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

Para obter mais informações, consulte [Anúncio de fallback para anúncios](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md)VAST e VMAP.

* **Biblioteca do Video Heartbeats (VHL) atualizada para a versão 1.5**
   * Capacidade de enviar metadados com start de vídeo e/ou start de vídeo/anúncio/capítulo como dados de contexto
   * Menos tráfego de rede - As pulsações são menores em média e menores em tamanho

**Versão 1.4.7**

* **Suporte para individualização no local** Suporte para instalações no local do servidor de individualização do Adobe para personalizar a solicitação de individualização do cliente para acessar um terminal diferente.

**Versão 1.4.6**

* **Criptografia AES de amostra (requer a versão 17.0.0.134 do Flash Player)**A criptografia AES baseada em amostra agora é suportada.

**Versão 1.4.2**

* **Atualização da Biblioteca do Video Heartbeats (VHL) para a versão 1.4.0.1**

   * Adicionada a capacidade de agrupar diferentes casos de uso de análises, de outros SDKs ou players, com o Adobe Analytics Video Essentials.
   * O rastreamento de anúncios foi otimizado com a remoção dos métodos trackAdBreakStart e trackAdBreakComplete. A quebra de anúncio é inferida das chamadas de método trackAdStart e trackAdComplete.
   * A propriedade playhead não é mais necessária ao rastrear anúncios.

* **Integração** do SDK NielsenO TVSDK agora oferece suporte ao envio de informações de rastreamento do usuário para o SDK Nielsen sem qualquer integração personalizada.

**Versão 1.4.0**

* **Sinalização de Blecaute com Substituição** de Conteúdo Alternativa Como parte da atualização 1.4 do TVSDK, o TVSDK também oferece suporte para entrar e retornar de blecautes regionais contra conteúdo linear. O TVSDK agora pode processar dois arquivos manifest em paralelo, principal e alternativo, para monitorar sinais de blecaute mesmo quando programação alternativa estiver sendo mostrada no lugar da programação original.

* **Remova/substitua anúncios** C3 Agora, nenhum trabalho de preparação adicional é necessário para inserir dinamicamente novos anúncios nos ativos VOD (Video-on-demand) que saem da janela C3. O TVSDK agora fornece uma API para remover intervalos de conteúdo personalizados e inserir dinamicamente novos anúncios. Essa nova funcionalidade poderosa também é útil em casos em que o conteúdo ao vivo/linear é exibido durante a transmissão e é imediatamente suspenso para uso como conteúdo sob demanda sem tempo adequado para &quot;limpar&quot; o ativo.

* A interface PlaybackEventListener tem um novo método chamado onReplaceMediaPlayerItem, que você pode usar para ouvir um novo evento `ITEM_REPLACED`. Esse evento é despachado sempre que uma instância MediaPlayeritem é substituída no MediaPlayer. O aplicativo cliente que está implementando este PlaybackEventListener deve implementar ou substituir esse novo método.
* AdClientFactory tem uma nova função adicionada à classe para registro em vários Detectores de Oportunidade:

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

* A interface PlaybackEventListener tem um novo método chamado onReplaceMediaPlayerItem, que pode ser usado para acompanhar um novo evento, ITEM_REPLACED. Esse evento é despachado sempre que uma instância MediaPlayeritem é substituída no MediaPlayer. O aplicativo cliente que está implementando este PlaybackEventListener deve implementar ou substituir esse novo método.

* AdClientFactory tem uma nova função adicionada à classe para registro em vários Detectores de Oportunidade:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Por exemplo, para o recurso de saída de anúncio inicial, você precisa de dois Detectores de oportunidade: um para inserção de anúncio e outro para saída antecipada do anúncio.

Para substituir essa nova função, crie um único Detector de oportunidade, coloque-o em um storage e volte:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Certificação e suporte de dispositivos no 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Os seguintes recursos **não** são suportados no TVSDK:
>
>* Movimentação lenta, em qualquer plataforma ou versão.
>* Brincadeira ao vivo.


**Versão 1.4.43**

O TVSDK 1.4.43 foi certificado com dispositivos Android com Android 6.0.1/ 7.0 e 8.1 (Oreo).

* **Versão 1.4.23:**

   * O TVSDK 1.4.23 foi certificado para dispositivos Android com Android N.

* **Versão 1.4.18:**

   * O Primetime foi certificado para Amazon Fire TV.
   * O VPAID 2.0 é compatível somente com dispositivos com Android 4.0 e superior.

## Problemas resolvidos no 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Todos os clientes TVSDK que usam CRS são altamente incentivados a atualizar para o TVSDK 1.4.39 ou mais recente no iOS e Android. Esta atualização é uma substituição instantânea da implementação do aplicativo existente. Após a atualização, verifique as solicitações de URL criativo do CRS em uma ferramenta proxy (por exemplo, Charles) para verificar se a versão no caminho reflete a versão 3.1. Por exemplo:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versão 1.4.43**

* Ticket #27143 - Unable to play 5.1 audio track on FireTV devices

   * O TVSDK agora pode reproduzir áudio AC3 em dispositivos FireTV. A reprodução está sempre em estéreo.

* Ticket #33902 - Delivery de anúncio seguro em HTTPS

   * A Adobe Primetime fornece uma opção para solicitar a primeira chamada para o servidor de anúncios primetime e CRS em https.

* Ticket #34493 - Atraso de áudio Bluetooth

   * Adicionada `alwaysUseAudioOutputLatency` na classe MediaPlayer que, quando definida, resultará no uso da latência de saída de áudio no cálculo do carimbo de data e hora de áudio.

* Ticket #34949 - Nova versão da biblioteca de pulsação de vídeo (VHL) integrada.

**Versão 1.4.42 (1791)**

* Zendesk #33719: A taxa de bits adaptável FireTV 4k é dimensionada lentamente. Adicionado suporte para ABR para dispositivos FireTV 4K.
* Zendesk #33338:  resetDRM limpa todos os dados do aplicativo.  Casos extras tratados em que as exceções em threads que não são TVSDK estavam fazendo com que as filas de operação TVSDK fossem preenchidas.

**Versão 1.4.41 (1776)**

* Zendesk #33002 - Dados de ativos complementares do TVSDK na Fire TV. Implementação de uma nova classe AdBannerAsset que retornará os dados do Companion como Lista &lt;AdBannerAsset> e AdAsset::id agora é uma String em vez de longos.
* Zendesk #32821 - O Android Primetime player congela quando encontra o PTS (Presentation Timestamp, carimbo de data e hora da apresentação) para WWE. Esse problema foi corrigido nesta versão.
* Zendesk #33572 - VideoAnalyticsFalha no Start do anúncio do provedor. O uso da combinação correta da versão SDK conjunta VHL+Nielsen do VideoHeartbeat.jar corrigiu esse problema.
* Zendesk #33355 - Fire TV: Volte com 15 segundos. Nenhuma correção do lado do TVSDK e o cliente estão verificando isso em seus Termos finais e terceiros.

**Versão 1.4.40 (1764)**

* Zendesk #33068 - Problema de sincronização de lábios do Amazon em um novo dispositivo. Problema de sincronização de lábios foi corrigido nessas versões.
* Zendesk #32215 - Android TVSDK 1.4.38 Problemas de segurança `[Hotlist]`. Atualizado para o OpenSSL-1.1.0 e o curl-7.55.1 mais recentes.
* Zendesk #32920 - Tela em branco em uma pausa de anúncio e sem a conclusão de uma pausa de anúncio. Correção de um problema em que um container VPAID poderia entrar em um estado suspenso e lidar com um problema em que os anúncios VPAID do Facebook costumavam retornar vários blocos CDATA em um único \&amp;lt;AdParameters\&amp;gt; nó VAST.

**Versão 1.4.39 (1744)**

* Zendesk #28976 - A solicitação de licenciamento demora mais de um segundo. Enquanto as chamadas de solicitação de licença de DRM que usam o POST estão sendo executadas, o Curl adiciona &quot;Expectativa: 100-continue&quot; cabeçalho. Removido o cabeçalho &quot;Expect:&quot; no TVSDK.
* Zendesk #27707 - ambientes CSAI que não cumprem os marcadores CUE IN para retorno antecipado ou retorno ao conteúdo. Suporte fornecido para vários geradores de oportunidade.

**Versão 1.4.38 (1722)**

* Zendesk #21590 - Desempenho e rastreamento de vídeo nas mais recentes compilações de Origem

Integração e certificação do VHL 2.0 no TVSDK para reduzir a barreira na implementação da Biblioteca do VideoHeartbeats diminuindo a complexidade das APIs.

* Zendesk #29688 - Suporte para clientes Android O Beta.

Suporte TVSDK para a nova versão beta do Android.

**Versão 1.4.36 (1713)**

* Zendesk #27392 - Ignorar conteúdo no Android

Para acomodar a descriptografia, o Android TVSDK estava ampliando incorretamente o intervalo de bytes do conteúdo não iframe em 16 bytes. O alargamento é necessário para fluxos Iframe, mas não para fluxos sem iframe.

**Versão 1.4.34 (1702)**

* Zendesk #27638 - vazamento no objeto cURL INet

O objeto Posix cURL INet vazava enquanto permanecia no gerenciador de compartilhamento e no cache DNS usado nas conexões cURL.

Esse problema foi resolvido ao excluir o objeto Inet cURL do Posix do desconstrutor INet.

**Versão 1.4.33 (1694)**

* **Biblioteca OpenSSL**

A biblioteca OpenSSL foi atualizada com a versão 1.0.2j do OpenSSL.

* Zendesk #21701 - Envia o URL criativo original para a solicitação CRS 1401 em vez do URL normalizado.
Esse problema é resolvido enviando os URLs criativos originais.

* Zendesk #25023 - Reprodução de vídeo de longa duração: congelamento de vídeo, oscilações de telaEsse problema foi solucionado definindo as dimensões máximas de formato de vídeo para dispositivos de decodificadores CenturyLink.

* Zendesk #27460 - A nova conta do Akamai não consegue lidar com uma solicitação de cdn de POST.
O código foi atualizado para fazer com que o `cdn.auditude.com` anúncio seja GET em vez de POST.

* Zendesk #28245 - O estado de reprodução não é notificado corretamente quando o aplicativo vai do plano de fundo para o primeiro planoEsse problema foi resolvido restaurando corretamente o estado de reprodução para reproduzir ou pausando quando o aplicativo retorna ao primeiro plano.

**Versão 1.4.32 (1682)**

* Zendesk #25779 - A vulnerabilidade de segurança encontrada com TVSDKAndroid 4.2 e anterior apresenta uma vulnerabilidade de segurança quando o JavaScript está ativado em um WebView. O uso do WebView por TVSDK foi desabilitado para dispositivos que executam o OS 4.2 ou inferior. Isso desativa o uso de anúncios VPAID no TVSDK nesses dispositivos.

* Zendesk #26890 - Problema no estado da TELA (ATIVADO/DESATIVADO) ao manipular Ref. PlayerQuando o mecanismo de vídeo Adobe (AVE) retoma de um estado SUSPENDER, o DefaultMediaPlayer não atualiza seu status. Como resultado, o DefaultMediaPlayer permanece em um estado SUSPENDER mesmo que o AVE esteja em um estado PLAYING. Esse problema foi resolvido ao configurar o estado DefaultMediaPlayer para PLAYING ao receber um status PLAY do AVE, mesmo se o status atual do DefaultMediaPlayer for SUSPENDER.

**Versão 1.4.31 (1675)**

* Zendesk #21974 - Exceções devido a objetos nulos
   * AdIndex raramente aumenta quando nulo. Isso pode ocorrer devido a chamadas de API incorretas recebidas para o adBreak precedente. Correção dos tipos de dados para evitar exceções

* Zendesk #24714 - Desativar registro em log de erros
   * O TVSDK foi atualizado para desativar o registro em log externo

* Zendesk #24488 - Problemas de sincronização AV na Fire TV
   * Correção ao melhorar a manipulação dos processos do decodificador AV. Especificamente, sempre que as filas de quadros de entrada ou de saída são modificadas, o thread decodificador específico para o tipo de conteúdo do quadro é executado.

* Zendesk #26551 - Corrigir as falhas do CRS
   * Quando a solicitação é HEAD (http head), não precisamos ler o conteúdo porque ele está vazio. Embora esteja certo tentar ler, o Android antigo (4.0.x) trava enquanto chamamos read() e o Android mais recente retorna o valor correto (-1) quando chamamos read(). Com base nisso, o código foi alterado para não ler o conteúdo para &quot;head&quot;

* Zendesk #26696 Nulo - Exceção de ponteiro ao acessar TrickPlayManager
   * Corrigido verificando se o objeto TrickPlayManager não é nulo antes de usá-lo.

**Versão 1.4.30 (1659)**

* A duração do ativo do Zendesk #22675 não é atualizada para fluxos ao vivo/linearesEsse problema foi resolvido fornecendo uma nova API, assetDuration, em PTVideoAnalyticsTrackingMetadata que fornece a duração do ativo para fluxos ao vivo e linear.

* Zendesk #25853 Falha de memória no TVSDK ao alternar canaisO problema no qual um buffer de leitura de arquivo vaza quando o MediaPlayer é redefinido ou liberado durante o download de um arquivo foi resolvido.

**Versão 1.4.29 (1653)**

* Zendesk #21200 - O player não se recupera do estado suspenso quando o aplicativo estava em segundo planoQuando o player foi suspenso após a sinalização do switch de fluxo, a resolução permite que o player execute o switch de fluxo ao restaurar o player do estado de suspensão, em vez de restaurar para a posição anterior.

* Zendesk #23412 - O Player fica preso a uma caixa preta se você clicar em qualquer Anúncio nos últimos 3s do intervalo do anúncioEsse problema é igual ao Zendesk nº 21200.

* Zendesk #23616 - Quebra de linha de anúncio ignorada procura muito no futuroDependendo do tipo de inserção do anúncio (inserir/substituir), o TVSDK determina se a duração do anúncio é usada no cálculo para determinar o ponto final de quebra do anúncio.

* Zendesk #25078 - TVSDK DRM Memory vazamento de memória na TV AndroidO vazamento de memória do objeto do adaptador DRM foi localizado e corrigido.

* Zendesk #25067 - Travamento em VideoEngineLinha do tempoIsso ocorre porque os objetos não foram limpos corretamente e os eventos foram chamados depois que os objetos foram destruídos. O problema foi resolvido adicionando verificações para evitar exceções nulas.

* Zendesk #25352 - Definir cabeçalho HTTP personalizadoEsse problema foi resolvido adicionando um novo cabeçalho personalizado à lista de permissões no TVSDK.

* Zendesk #25617 - Rollover PTS de fluxo ao vivo, causando descontinuidade do player e falha de memóriaEsse problema foi resolvido com a adição de uma sobreposição PTS em FragmentadoHTTPStreamer quando uma sobreposição ocorre no meio de um segmento.

**Versão 1.4.28 (1637)**

* Zendesk #23618 - eventos de quebra de anúncio são acionados antes da política de publicidade. Esse problema foi resolvido ao não disparar os eventos AD_BREAK_START e AD_START quando o anúncio é ignorado por causa do adForgiveness. Em vez disso, o evento AD_BREAK_SKIPPED é enviado.

**Versão 1.4.27 (1631)**

* Zendesk #23174 - Problema de desempenho ao redimensionar o vídeoEsse problema foi resolvido ao comprovar uma nova API, MediaPlayerView.setSurfaceFixedSize, que permite que o TVSDK acesse SurfaceHolder.setFixedSize() de MediaPlayerView.

* Zendesk #24450 - TVSDK faz duplicados e solicitaçõesEsse problema ocorria quando o tempo decorrido era convertido em longo e não em duplo, e esse problema foi corrigido.

**Versão 1.4.26 (1627)**

* Zendesk #21436 - Atualização da biblioteca OpenSSL para a versão 1.0.2h Atualização da biblioteca OpenSSL para OpenSSL versão 1.0.2h
* Zendesk #23825 - Os cookies não estão sendo incluídos nos retornos de chamada Corrigidos fornecendo suporte para cookies do Android.

**Versão 1.4.25 (1620)**

* Zendesk #22900 - O fluxo DRM ao vivo do Adobe Primetime não está sendo reproduzido no player de referência do AndroidO problema de alocação de memória foi corrigido.
* Zendesk #23176 - O aplicativo trava ao tentar reproduzir anúncios VPAIDA falha ocorreu porque o aplicativo não cria uma visualização de anúncio personalizada para renderizar um anúncio VPAID. Esse problema foi resolvido ignorando os anúncios VPAID na resposta do servidor de publicidade quando não há visualização de anúncio personalizada.

* Zendesk #23153 - SampleAES DRM Stream - Playback stalling in the TVSDK Reference PlayerEsse problema é igual ao Zendesk #22900.

**Versão 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Acionar conclusões de conteúdo para transições de vídeo ao vivoEsse problema foi resolvido com a adição de uma API (trackVideoComplete) para acionar manualmente a conclusão do conteúdo durante uma sessão de rastreamento de vídeo ao vivo/linear.

* Zendesk #21977 VideoEngineFalha na linha do tempo durante a operação placeAdBreak/acceptAd
   * Neste problema, as seguintes bibliotecas foram atualizadas:
      * Biblioteca do AdobeMobile para a versão 4.10.0
      * Biblioteca VHL para a versão 1.5.6
      * Biblioteca VHL-Nielsen para a versão 1.6.7

Esse problema foi resolvido adicionando uma verificação nula antes de adicionar publicidades à lista de publicidade aceita.

* Zendesk #22313 A taxa de bits para STBs com chipset Amilogic não vai além de 1.2MTesse problema foi resolvido com o pré-carregamento dos recursos de codec de mídia e a desativação do switch integrado para dispositivos de chipset Amilogic.

* Zendesk #19520 AES HLS de amostra não reproduzido em players TVSDKEsse problema foi resolvido com a manipulação de vários descritores PMT para fluxos HLS criptografados AES de amostra.

**Versão 1.4.23 (1602)**

* Zendesk #18852 - Atualizar lógica de seleção criativa com base nas regras do CRSEsse problema foi resolvido adicionando um arquivo de configuração JSON para especificar a prioridade de seleção criativa.

* Zendesk #20861 - Android NTEsta versão oferece suporte para Android N, removendo a capacidade de usar diretamente as bibliotecas nativas da plataforma Android que não estão mais acessíveis aos aplicativos executados no Android N.

* Zendesk #21018 - Android N crashMesma resolução que ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter falha em um erro Invalid_KeyO erro Invalid_Key não inclui uma descrição do AVE, portanto, analisar o texto resultou em NPE. O problema foi resolvido adicionando uma verificação nula para a descrição durante onError antes de analisar a descrição.

* Zendesk #22286 - A biblioteca nativa está alocando a chave/fragmento de leitura de memória causando falhasEssa falha que ocorreu no Android ao tentar carregar um manifesto com várias chaves simultaneamente foi corrigida.

**Versão 1.4.22 (1581)**

* Zendesk nº 17236 - Tempo de reprodução não confiável para vídeos HLS com DRMTo salto de tempo com os streams LBA, onde o tempo de start do segmento de áudio não corresponde ao tempo de start do segmento de vídeo, foi corrigido.

* Zendesk #17680 - A reprodução de vídeo está congelando na caixa Selevision AndredoO decodificador de vídeo neste dispositivo às vezes retorna um salto significativo no tempo de saída ao desenfileirar quadros de vídeo do buffer de saída, e esse carimbo de data e hora de saída permanece alto. Esse problema foi resolvido retornando um erro de perfil de *vídeo não suportado* que não força o player a tentar novamente o mesmo perfil ou a escolher outro perfil.

* Zendesk #19074 - Congelamento de vídeo durante reprodução de truques FFWD e REWesse problema foi resolvido com a adição de um novo aviso TRICKPLAY_ENDED_DUE_TO_ERROR para notificar ao aplicativo que o recurso de trickplay saiu e que o vídeo foi pausado devido a um erro irrecuperável.

* Zendesk #19574 - TVSDK não está retornando dados de resposta M3U8 para conteúdo DRM ou não DRMEsse problema foi resolvido das seguintes maneiras:

* Zendesk #19986 - Comportamento de OP quebrado para certos dispositivos como Android TV
* Adicionando um erro FILE_NOT_FOUND à condição.
* Quando o erro vem de um erro de *arquivo não encontrado* , separando o URL e a resposta da descrição do erro se a resposta estiver disponível.
O erro de lógica introduzido pelo suporte a NVidia shield OP foi corrigido. Em dispositivos blindados não NVidia, confie nos sinalizadores protegidos de exibição mesmo quando o tipo de exibição for desconhecido.

* Zendesk #20549 - Manuseio de listas de reprodução obsoletas. Esse problema foi resolvido reduzindo o intervalo entre a atualização do manifesto ao vivo para metade da duração esperada do segmento, se a busca anterior não receber novos segmentos.

* Zendesk #20742 - O uso de memória parece continuar aumentando ao reproduzir conteúdo ao vivo no FireTV. A falha é causada pela tabela de referência de objeto JNI que atingiu o limite. Esse problema foi resolvido ao excluir a referência ao objeto MediaFormat que foi criado durante a reinicialização do decodificador.

* Zendesk #21125 - Retorno de live/linear e quebra antecipada (CSAI). Adicionado um recurso que permite ao player retornar ao conteúdo principal durante uma pausa de anúncio se o player registrar a divisão em dicas de anúncio usando a divisão no detector de oportunidade.

* Zendesk #21334 - TVSDK valor de tempo limite de solicitação de anúncio para solicitação de anúncio de terceiros. Uma configuração adRequestTimeout foi adicionada a AdvertisingMetadata que permite um tempo limite global para a chamada de anúncio.

**Versão 1.4.21 (1566)**

* Zendesk #17781 - Captura de tela do ADB não funciona maisEsse problema foi resolvido com a adição da API DefaultMediaPlayer.create(Context context, boolean secureSurface), que permite a captura de tela.
Para permitir capturas de tela, passe false para secureSurface.
Importante: Recomendamos que você não ative esse recurso de captura de tela em uma configuração de produção.

* Zendesk #19074 - Video congelar durante reprodução de truques FFWD e REWos seguintes problemas que ocorreram quando o trickPlay podia congelar no playback foram resolvidos:

* Zendesk #19532 - Close Caption is appear out of order
   * Os start FHS são reproduzidos, mas o primeiro segmento do iframe não tinha um quadro nele.
   * Durante o download de um segmento iframe, se o FHS atingir uma condição de erro, ele sairá do trickplay e pausa a reprodução.
   * A implementação do Android MediaCodec aguarda sempre a disponibilidade da fila de entrada enquanto foi solicitado que todos os buffers de entrada/saída fossem liberados.
Esse problema foi solucionado ao reverter a ordem das dicas WebVTT para que várias dicas sobrepostas pareçam &quot;rolar para cima&quot;.

* Zendesk #19574 - O TVSDK não retorna dados de resposta M3U8 para conteúdo DRM ou não DRMNa carga inicial do arquivo manifest em PTMediaPlayerItem.prepareToPlay, se o carregamento falhar, o TVSDK não reportará o corpo da resposta de falha ao aplicativo.
Esse problema foi resolvido permitindo que o TVSDK relatasse a resposta da falha como um erro para o aplicativo.

* Zendesk #19701 - Congelamento de reprodução com SAP/DescontinuidadeO reprodutor congela quando o áudio e o vídeo estão desalinhados na descontinuidade foi resolvido.

* Problema #PTPLAY-11162 - A atualização da biblioteca OpenSSL para a versão 1.0.2f foi solucionada.

**Versão 1.4.20 (1546)**

* Zendesk #17384 - Solicitação de recurso: O suporte a metadados ID3 para reprodução do AAC O suporte para tags ID3 em mídia do AAC foi fornecido no TVSDK para Android a partir da versão 1.4.20.

* Zendesk #18358 - O Player congela o switch de taxa de bits com descontinuidades fora de sincronização. Esse problema foi solucionado manipulando adequadamente os casos de borda de costura ABR.

* Zendesk #19232 - O aplicativo que usa o TVSDK 1.4.18 está se comportando estranhamente na versão mais antiga do Amazon OS 4Esse problema foi resolvido com a remoção da criação de visualização da Web oculta no processo de inicialização do TVSDK player para evitar conflitos com dispositivos que não suportam o Android Webview.

* Zendesk #19585 - Reprodução de movimento lento quando ocorre transição adaptável de taxa de bits.
Durante o switch ABR, se o novo perfil tiver uma taxa de amostra de áudio diferente do perfil atual, a reprodução se tornará rápida ou lenta. Isso ocorre porque o apresentador de vídeo não é notificado de que o formato de áudio foi alterado.
Esse problema foi resolvido garantindo que o sinalizador de notificação estivesse definido no local correto.

* Zendesk #19683 - SAP DAI playback - Sem áudio por alguns segundos.
Para vários casos na lógica do TVSDK, quando o carimbo de data e hora de dois segmentos de renderização foi comparado, RENDITION_TIMEOUT_THRESHOLD foi usado como um intervalo de valor aceitável, porque o carimbo de data e hora nem sempre pode ser combinado com uma diferença de 0 ms. Se a lacuna estiver dentro do intervalo de RENDITION_TIMEOUT_THRESHOLD, presume-se que é uma correspondência.

O RENDITION_TIMEOUT_THRESHOLD foi definido como 100 ms, mas foi considerado insuficiente para determinados fluxos. Esse problema foi resolvido aumentando RENDITION_TIMEOUT_THRESHOLD para 200 ms.

* Zendesk #19699 - O TVSDK falha ao alternar entre as faixas de legendas VTTEsse problema foi resolvido fazendo o player despejar e recarregando o manifesto quando um rastreamento é alterado e corrigindo o problema de conversão de string UTF8 que afetou os nomes de rastreamento de legendas WebVTT de duplo byte.

* Zendesk #19717 - Opções CC exibe um problemaEsse problema foi resolvido manipulando corretamente a sequência Unicode.

* Zendesk #19910 - TTI2 ID3 tags not detected Esse problema foi resolvido fornecendo suporte mais completo para codificações de sequência de caracteres ID3 v2.4 e para suporte a ID3 v2.3.

* Zendesk #20135 - O TVSDK está acionando vários onComplete para conteúdo VOD.
Esse problema foi resolvido com a adição do ouvinte de eventos post_roll_complete no local certo, em vez de no caso completo do evento de alteração de status.

**Versão 1.4.19 (1521)**

* Zendesk #4180 - O TVSDK não está impondo o HDCP.
   * Essa é uma correção parcial para esse ticket e resolve apenas o problema dos dispositivos de blindagem NVidia.
Você deve usar a API de detecção HDCP corretamente implementada no Nvidia Shield para rastrear dinamicamente o status HDCP.

* Zendesk #18358 - O TVSDK congela no switch de taxa de bits com descontinuidades fora de sincronização.
   * Esse problema foi resolvido adicionando um novo aviso para detectar a descontinuidade do PTS e forçando a verificação do PTS a refazer a pesquisa pelo segmento correto para cada switch ABR.
Para corrigir o congelamento, a chamada para o método mediaPlayer.setCustomConfiguration deve incluir forcePTSCheckForABR como um argumento.

* Zendesk #19038 - Sem fluxo ao vivo no Asus Zenpad 10.

   Esse problema foi resolvido ao pré-carregar as informações do codec de mídia, para que você não query a função em tempo de execução.

* Os seguintes problemas são os mesmos do Zendesk #19038:
   * Zendesk #19483 - O TVSDK está falhando na plataforma Intel.
   * Zendesk #19171 - Travamentos no Asus Memo Pad 7 com Android 5.0.

**Versão 1.4.18 (1503)**

* Zendesk #3324 - O relatórios de anúncios do Primetime não rastreia quebras de anúncios quando não há mídia de anúncio em um VMAP.
Quando uma pausa de anúncio está vazia, o start de pausa do anúncio e os eventos de rastreamento completos não estavam sendo vinculados. Esse problema foi resolvido enviando start de quebra de anúncio em intervalos vazios de anúncios, como VMAP AdBreak, com um nó AdSource válido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) é ignorado após a chamada MediaPlayer.reset(). Esse problema foi resolvido com a adição de setCCVisibility(Visibility.INVISIBLE); para a função reset() na classe MediaPlayer.

* Zendesk #18328 - Problema de quadro ignorado nos dispositivos de segunda geração da Amazon Fire TV para o conteúdo com 60FPSTesse problema foi resolvido aplicando o FPS codificado para a tomada de decisão do tempo de espera e com uma lógica de previsão FPS melhor codificada.

**Versão 1.4.17 (1472)**

* Zendesk #2231 - Erro retornado ao buscar o manifesto indisponível em MediaPlayerNotificationEsse problema foi resolvido incluindo o corpo da resposta do manifesto quando há um erro de análise.

* Zendesk #17703 - VideoEngineView não impede capturas de tela durante a reprodução do vídeoO método setSecure está disponível desde a API 17, mas como a API 17 abrange as seções 4.2, 4.2.1 e 4.2.2, não se sabe qual lançará uma exceção ou se é específica do dispositivo. Esse problema foi resolvido vinculando VideoEngineView.setSecure à cláusula try catch.

* Zendesk #17919 - A busca de conteúdo causa erro de pulsaçãoUm erro de dados de entrada inválido estava ocorrendo como resultado da chamada de pulsação que foi gerada quando a busca foi iniciada após a pré-rolagem. Esse problema foi resolvido.

**1.4.16a** (1454a)

* Zendesk #18215 - Alguns fluxos AES não podem ser carregados.
Esse problema foi resolvido verificando o tamanho dos metadados do DRM do perfil antes de carregar a chave AES.

**Versão 1.4.16 (1454)**

* Zendesk #3875 - Tab S Crash durante a reproduçãoReverter a dependência de OKHTTP no Auditude para CRS porque o TVSDK agora está usando diretamente httpurlconnection em vez de ondulação. O problema foi resolvido com a compensação de exceções antes de qualquer outra chamada JNI.

* Zendesk #4487 - Tracking Linear Canal of ContentO problema foi resolvido permitindo a reinicialização do rastreador de pulsação de vídeo durante uma sessão de reprodução de fluxo linear.

* Zendesk #17919 - Android - busca de conteúdo causa erro de pulsaçãoO problema quando a pulsação está em um estado de erro quando há uma busca em um capítulo foi resolvido.

* Zendesk #18053 - Adobe Primetime falha no MarshmallowO TVSDK travava no Android M OS quando a biblioteca do TVSDK usava código neon que faz a conversão de cores YUV -> RGB. O problema foi resolvido atualizando as funções que estão causando esse problema usando a versão não neon do código.

* Zendesk #18072 - Android M - Falha do aplicativoAo verificar se o perfil e o nível são suportados, ocorre uma falha ao chamar as APIs MediaCodecList e MediaCodecInfo. O problema foi resolvido fornecendo uma solução temporária carregando todas as informações do codec antecipadamente para evitar chamar essas APIs somente quando as informações do codec forem necessárias.

* Zendesk #18074 - Legendas árabes que não funcionam no Nexus com Android 6.0 O problema foi resolvido fornecendo suporte ao mapa de fontes CTS para Android.

**Atualização da versão 1.4.15 (1438)**

* Zendesk #17437 - Atraso longo na inicialização do conteúdo VOD com alguns fluxos AES.
Para resolver esse problema, se várias chaves listadas no manifesto, baixe todas as chaves AES em paralelo.

**Versão 1.4.15 (1435)**

* Zendesk #4278 - Falhas no Android definem as caixas superiores quando a taxa de bits adaptável muda (ABR).
A correção foi adicionar suporte para o switch ABR integrado com o codec de mídia Android mais recente.

* Zendesk #17063 - Chamar mediaPlayer.reset() causa um erro de reinicialização do mecanismo de vídeo.
A correção era incluir o MediaErrorCode original de VideoEngineExceptions ao despachar ErrorEvents.

* Zendesk #17130 - Uma breve, mas notável, pausa ao mudar a taxa de bits vista no FireTV.
(Igual a #4278 acima) A correção foi adicionar suporte para o switch ABR integrado com o codec de mídia Android mais recente.

* Zendesk #17666 - Marcadores de anúncios adicionais, Inesperados ou Sem anúncios ao retomar o conteúdo.
A correção foi um problema ao fazer o conteúdo prepareToPlay on video-on-demand (VOD), a busca inicial é executada no horário local em vez do horário virtual.

* Zendesk #17437 - Atraso longo na inicialização do conteúdo VOD com alguns fluxos AES.
A correção foi baixar todas as chaves AES em paralelo quando várias chaves estão listadas no manifesto.

* Zendesk #17851 - Android TV - Quadro preto durante ABRTa correção era especificar KEY_MAX_WIDTH e KEY_MAX_HEIGHT para ativar a reprodução adaptável.

**Versão 1.4.14 (1415)**

* Zendesk #3875 - Tab S Crash durante a reprodução.
Foi necessária uma correção adicional para evitar a falha.

* Zendesk #17245 - Fallback on Android TV não está funcionando.
Corrigido um problema adicional no qual a reprodução travava quando o fallback estava ativado e a resposta VMAP tinha uma pausa de anúncio vazia.

**Versão 1.4.14 (1412)**

* Zendesk #17245 - Fallback na TV Android não está funcionando.
Removida uma restrição para desativar a reembalagem criativa em anúncios de fallback.

**Versão 1.4.13 (1388)**

* Zendesk #3502 - Suporte a failover baseado em cliente HLS durante uma quebra de anúncioPermita o failover para o manifesto principal ao atualizar o erro de perfil ativo durante o período de interrupção do anúncio.

* Zendesk #3875 - Tab S Crashes during playbackPara resolver o conflito entre HttpUrlConnection e cURLm, use uma biblioteca de terceiros.

* Zendesk #4450 - edição de configuração de metadados personalizados para uma única disposição em um resolvedor de conteúdoAdicione um definidor às configurações de Oportunidade.

**Versão 1.4.12 (1388)**

* Zendesk #2751 - CSAI e CRS | Reforço: Tratar elementos dinâmicos em determinados URLs de arquivos de mídia.
Serviço de reempacotamento da Creative para lidar corretamente com anúncios com URLs criativos dinâmicos.

* Zendesk #3965 - Alternar para a reprodução normal a partir do trickplay resulta em um salto para frente um pouco antes de iniciar a reprodução.
   * A correção inclui o TVSDK que retorna o tempo antes da alteração da taxa até que todas as variáveis sejam atualizadas, em vez de tentar calcular o GetStreamTime.
   * Corrigida uma falha ao alterar a velocidade de reprodução do truque próximo ao final do fluxo.
   * Cálculo de tempo atual corrigido durante a reprodução do truque.

* Zendesk #3978 - Trickplay às 8x e 16x frequentemente congela.
   * Sempre escolha o perfil de execução de truque com a menor taxa de bits para evitar o buffer constante.
   * Aumente o intervalo de quadros ignorados para obter uma alta taxa de execução de truques.
   * Correção de um problema em que o buffer continua crescendo após atingir a duração do público alvo durante a reprodução do truque.

* Zendesk #3992 - Velocidades adicionais do Trickplay.
O TrickPlay foi atualizado para aceitar taxas superiores a 16x; +/- 32, +/-64 e +/-128 agora também são permitidos.

* Zendesk #4007 - Interpretação do objeto GEOB como parte dos metadados da linha do tempo (Android e Web).
Adicionada a API setByteArray e getByteArray.

* PTPLAY-7301 - Instant On start no ponto de acesso aleatório.
O Instant On foi atualizado para permitir um ponto de partida diferente de zero.

**Versão 1.4.11 (1363)**

* Zendesk #2076 - Frequent stutter when play video on Motorola Xoom with Android 4.0.3Adição de dispositivos à lista de permissões para impedir que eles tentem reproduzir conteúdo de perfil alto.

* Zendesk #2197 - Tracking ad errorsdispatOperationFailedEvent com notificação de aviso. `[Ads]`

* Zendesk #3304 - macro VAST 3.0 `[ERRORCODE]` não sendo preenchida
   * o código de erro 400 será exposto se o anúncio em linha apresentar anúncios mal criados.
   * `[ERRORCODE]` macro será codificada em URL

**Versão 1.4.10 (1354)**

* Zendesk #2941 - Os ativos ao vivo não têm &quot;0&quot; no intervalo pesquisávelAnteriormente, havia um buffer de 3 segmentos ao buscar o início de um fluxo ao vivo, agora é possível buscar o início de um fluxo ao vivo (ou seja, o start do primeiro segmento).

* Zendesk #3169 - Atualizar player de referência com integração com Adobe AnalyticsO player de referência foi atualizado com a biblioteca do Adobe Analytics como exemplo de implantação.
* Zendesk #3299 - Comportamento inexplicável da peça
   * Correção de um bug no qual retornar ao estado de reprodução após a interrupção da reprodução de truques poderia levar vários segundos (às vezes, mais de 25 segundos).
   * Correção de um erro em que invocar a reprodução de truque uma segunda vez na mesma mídia pode fazer com que o fluxo congele no momento atual.
* Zendesk #3433 - Android e Flash - Problemas com legendas

GetLine para WebVTT não respeitava um comprimento ajustado de &lt;CR>&lt;LF> para um pacote; a última legenda pode conter caracteres de legendas anteriores.

* PTPLAY-6243 - Aprimorar o player de referência para capturar informações de depuração

Os players de referência de amostra do Android foram aprimorados com uma opção para ativar os logs de depuração e enviar os resultados por email. Essa opção é encontrada no menu Log no player de referência.

**Versão 1.4.9 (1332)**

* Zendesk #2649 - Buffer Complete (Buffer concluído) ocorre antes do buffer inicial estar cheio

Após uma busca, caso possível em que o mecanismo de vídeo defina o estado como REPRODUÇÃO antes que o apresentador de vídeo esteja pronto para reproduzir. Ocorre quando o estado do buffer é alto antes da busca. Correção notificando o mecanismo de vídeo de estado de buffer baixo. Com o estado de buffer baixo do mecanismo de vídeo, chamar Play faz com que o estado mude para BUFFERING em vez de PLAYING. A reprodução é retomada quando o estado é alterado para REPRODUÇÃO.

* Zendesk #2846 - Solicitação de aprimoramento: Fornecer a capacidade de definir uma sequência diferente de agente do usuário para chamadas feitas pela biblioteca do Auditude

Uma nova API foi adicionada para definir o agente do usuário para chamadas relacionadas a anúncios, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Se nenhum agente do usuário estiver definido, o padrão será usado. Isso afeta apenas o agente do usuário para chamadas relacionadas a anúncios, o agente do usuário para chamadas de mídia não é alterado, que é &quot;Adobe Primetime&quot;+&lt;default useragent>.

**Versão 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Erro com local ... Se o carregamento do manifesto em FragmentadoHTTPStreamer::ThreadParseManifest() falhar, verifique se o domínio do URL é localhost e, em caso afirmativo, altere o domínio para 127.0.0.1 e retorne ThreadParseManifest.
* Zendesk #3072 - Alternância automática para taxas de bits mais baixas. Alteração do cálculo de comprimento do buffer para ignorar a carga PTS zero.
* Zendesk #3168 - Legendas WebVTT exibidas somente para os primeiros 10 segundos.
* Zendesk #3193 - Solicitação de uma API de alteração de Perfil no TVSDK, PlaybackEventListener.onProfileChanged() foi adicionada.

**Versão 1.4.7 (1311)**

* Zendesk #2197 - Rastreamento de erros de anúncio. Falha ao carregar a notificação do ativo adicionada para o manifesto
* Zendesk #2575 - PSDK ignora o anúncio em fluxo personalizado MARK antes do vídeo
* Zendesk #2719 - Ganhe a morte com anúncios de auditude, rastreamento de sinal fixo quando redirecionado para URL relativo no plug-in de auditude
* Zendesk #2760 - Tag DISCONTINUITY ignorada durante o modo TrickPlay
* Zendesk #2805 - Player Crash at Beginning of Playback (Travamento do reprodutor no início da reprodução), mesma correção do Zendesk #2719
* Zendesk #2817 - Android player - O player às vezes trava e para de reproduzir, corrigido ao estender os buffers de decodificação de 2,0 para 3,0 segundos
* Zendesk #2839 - O Adobe Primetime PSDK suporta chipsets ARMv8?, adição da correção para falhas encontradas no Galaxy S6.
* Zendesk #2885 - Auditude Crashes playback, mesma correção da Zendesk #2719
* Zendesk #2895 - Falha do Live HLS consistentemente após 10 minutos de reprodução
* Zendesk #2925 - Feedback em relação à compilação dev do Android (1.4.5), em certos dispositivos quando colocamos o pacote na fila de entrada, se o PTS for negativo, o decodificador entra em um estado estranho, no qual sempre recebemos um PTS de saída negativo para pacotes futuros. A correção definirá o PTS de entrada como zero se for negativo para evitar esse problema.
* PTPLAY-4645 - Desative o suporte a criptografia RC4 no openssl. Há explorações conhecidas para RC4. Isso significa que, se for feita uma tentativa de conexão com um servidor que suporte apenas RC4, ocorrerá uma falha.

**Versão 1.4.6 (1282)**

* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede ruins, corrigidas pela remoção rápida da implementação do switch.
* Zendesk #2631 - Legendas árabes no Android: O texto em várias linhas aparece recortado, corrigido ajustando o tamanho da fonte para fontes árabes.
* Zendesk #2844 - Buffering na nota 4 e tempo de download do fragmento não são precisos.

Esse problema foi corrigido adicionando latência entre downloads de segmentos de vídeo no cálculo da largura de banda e a lógica de cálculo do tempo de download usando o tempo de ciclo de solicitação completo.

* Zendesk #2908 - Legendas árabes que não funcionam no Nexust 5, 6 e 7, corrigidas adicionando mais 2 fontes de fallback para scripts árabes.
* PTPLAY-4627 - atualizar Nielson appsdk para a versão 1.2.3.7
* PTPLAY-5084 - Suporte a failover de atualização do Manifest ao vivo Principal

**Versão 1.4.5 (1248)**

* Zendesk #1757 - Somente reproduções de áudio ou travamentos de reprodutor para algum perfil de taxa de bits de vídeo, travamento de Nexus 4 e Nexus 7 corrigido
* Zendesk #2072 - TimedMetadata for AdEvent não contém o URL completo apenas &quot;http&quot;
* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede precárias
* Zendesk #2256 - Acesso à Playlist Principal, PSDK atualizado para despachar eventos timedMetadata para marcas assinadas na lista de reprodução principal.
* Zendesk #2269 - Dois idiomas diferentes de legendas aparecem na tela ao mesmo tempo com WebVTT
* Zendesk #2417 - Player trying to download legendas before playback start, WebVTT estava usando a variável de número de segmento errada para a correspondência de número de segmento. Erros só apareciam para mídias que tinham índices de segmentos começando em zero.
* Zendesk #2470 - PSDK not return from SUSPENDED state when bitrate change occur after Suspensão (O PSDK não retorna do estado SUSPENDIDO quando ocorre uma alteração na taxa de bits após a suspensão). Em uma situação especial, quando a busca inteligente é chamada pelo RestoreGPUResource (o player restaura do estado de suspensão) e o switch de fluxo detectado antes disso, a busca inteligente não pode ser concluída e resultar em buffering constante.
* Zendesk #2451 - Legenda fechada &#39;bottom inset&#39;, adicionado o parâmetro &#39;bottomInset&#39; ao código de legenda
* Zendesk #2480 - desabilitando a otimização de redirecionamento HTTP 302, Adicionado suporte para a configuração da propriedade useRedirectUrl
* Zendesk #2486 - Beacons de terceiros
* Zendesk #2547 - Legendas árabes: O texto deve ser alinhado à direita e justificado

**Versão 1.4.4 (1195)**

* Zendesk #1158 - Falha na reprodução no Huawei Valiant (Y301A1)
* Zendesk #1709 - Tamanho de mídia incorreto e vídeo esticado
* Zendesk #1757 - Somente o áudio é reproduzido após a troca do perfil entre fluxos com dados spa/pps idênticos
* Zendesk #2095 - Status HTTP 307 (redirecionamento) faz com que o player de Adobe pare a reprodução
* Zendesk #2126 - evento TimedMetaData ausente para o último ADEVENT, as tags assinadas que existem após o último segmento não foram reportadas ao PSDK do AVE
* Zendesk #2227 - Lockups in VideoEngine nativeReset and nativePause
* Erro #3921755 - Atualização da biblioteca OpenSSL para a versão 1.0.1L

**Versão 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Legenda fechada ativada e desativada
* PTPLAY-1818 - A reprodução de truques de rebobinamento para no anúncio em vez de rebobinar depois dele
* PTPLAY-2736 - Uma legenda WebVTT exibida anteriormente é mostrada na tela quando um fluxo com legenda WebVTT é concluído
* PTPLAY-3773 - Um anúncio intermediário não é reproduzido quando a reprodução de fluxo é iniciada após a posição do anúncio

**Versão 1.4.2**

* Zendesk #1561 - Suporte a failover baseado em cliente HLS no tempo limite. Usará a data e hora do programa para solucionar o failover
* Zendesk #1590 - LoadInfo.MediaDuration é sempre 0 (não fixo apenas para áudio)
* Zendesk #1626 - Potencial vazamento de memória no player. Sem vazamento de memória real, o problema era que o NotificationHistory salvava as últimas 1000 notificações, que foi reduzido para 100.
* Zendesk #2192 - A taxa de bits nem sempre diminui em condições de rede precárias

**Versão 1.4.1 (1121)**

* Zendesk #1951 - Lockup in VideoEngine.nativeReset() on 4.0.x devices
* Zendesk #2064 - Native Crash SIGSEGV em dispositivos Android específicos baseados na Intel
* Zendesk #2075 - Lockup in VideoEngine.nativeReleaseGPUResource em dispositivos 4.0.xObservação: Esta compilação é ***necessária*** para suporte do Android 5.0 (Lollipop)
* Zendesk #1513 - Suporte para Android Lollipop
* Zendesk #1709 - Tamanho de mídia incorreto e vídeo esticado
* Zendesk #1871 - As legendas WebVTT desaparecem ocasionalmente e reaparecem ao visualizar um livestream com legendas WebVTT
* Zendesk #1996 - Nenhum marcador de linha do tempo é visto no PSDK 1.4.0
* Zendesk #2046 - Crash with PSDK 1.4.1.1113, travamento corrigido para fluxos ao vivo quando nenhum anúncio é retornado da auditude
* Bug #3769657 - Atualizar a versão do curl para 7.38.0
* PTPLAY-1575 - Quando o ABR reproduz start com fluxo apenas de áudio e depois muda para fluxo de áudio/vídeo, o vídeo nunca é renderizado enquanto o áudio continua
* PTPLAY-2499 - Atualizar para OpenSSL para a versão 1.0.1j para corrigir vulnerabilidades recentes
* PTPLAY-2632 - O vídeo não é recuperado após a reprodução média do anúncio ser concluído no Android Lollipop
* PTPLAY-2678 - Paradas de vídeo durante testes de longevidade ao vivo no Android Lollipop

**Versão 1.4.0**

* Zendesk #1024 - Recurso para remover anúncio do fluxo via manifesto
* Zendesk #1293 - Problema de seleção de faixa de legenda fechada.
* Zendesk #1590 - LoadInfo.MediaDuration é sempre 0, mediaDuration agora mostra o valor correto.
* Zendesk #1629 - player/aplicativo trava no fim da reprodução do anúncio no Galaxy S4
* Zendesk #1674 - ClosedCaption Not appear up, correct 708 caption display when 0x03 ETX codes is missing. (Zendesk #1674 - ClosedLegtion Não exibido, exibição correta da legenda 708 quando os códigos ETX 0x03 estiverem faltando.
* PTPLAY-2157 - Os estilos de legenda padrão foram retornados por getters mesmo se um estilo diferente tiver sido definido e verificado visualmente no stream. As propriedades de estilo de Legenda fechada agora mostrarão o valor para o qual foram definidas.

## Problemas conhecidos no 1.4 {#known-issues-in}

**Versão 1.4.31**

* PTPLAY-16803 - A legenda fechada não funcionará com conteúdo somente de áudio, pois o sistema de legenda precisa de vídeo para funcionar. Sem vídeo, não há dimensão viewport e, sem uma dimensão viewport, não é possível exibir gráficos para legendas.
* PTPLAY-1634 - A mesma tag assinada tem carimbos de data e hora diferentes em janelas ativas diferentes. Quando a janela ativa se move, a mesma tag deve ter os mesmos carimbos de data e hora. No entanto, às vezes, mesmo as mesmas tags têm carimbos de data e hora diferentes.
* PTPLAY-3197 - Falha com sinal de erro SIGSEGV 11 no dispositivo Acer Iconia após ~ 1 hora de reprodução contínua
* PTPLAY-3310 - Com um áudio com taxa de bits mais baixa, o áudio fica instável/instável no Acer Iconia
* PTPLAY-3355 - WIN DEATH crash on Motorola Xoom com 4.0.x após ~ 1 hora de reprodução contínua.
* PTPLAY-3557 - O rebobinamento em um intervalo de anúncios está fazendo com que o fluxo seja concluído
* PTPLAY-7079 - Janela de reprodução no cliente Android não funciona com o Secure Stop/Hard Stop
* Bug #3760144 - A resolução pode mudar ou parecer pulsar quando o fluxo é pausado em alguns dispositivos como Kindle Fire 7 e Samsung Galaxy Nexus. Observável apenas sob inspeção atenta
* Bug #3761170 - searchToLocal in Live with Ads não pode buscar novamente conteúdo de anúncio, o melhor para usar as APIs currentTime para fluxos ao vivo
* Bug #3763370 - Os fluxos ao vivo com anúncios exibirão ocasionalmente dois marcadores de anúncio próximos quando deveria haver apenas um. Esses marcadores de anúncio representam o mesmo anúncio, e somente um será reproduzido
* Erro #3763373 - O marcador de anúncio pode desaparecer brevemente ao buscar além de um anúncio em fluxos VOD. O marcador de anúncio é restaurado e não há outro efeito adverso na linha do tempo
* Alguns dispositivos têm problemas conhecidos de reprodução. Consulte Problemas de dispositivo [conhecidos em 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementação de referência - A reprodução de truque não é implementada no aplicativo de amostra
* Em alguns dispositivos Android TV, uma imagem preta pode ser vista devido à redefinição do decodificador nos seguintes pontos de transição:
   * modo de reprodução de entrada e saída
   * alternar entre faixas de áudio de ligação tardia
   * de um anúncio ao conteúdo principal.

**Versão 1.4.23**

* A Legenda fechada não funcionará com conteúdo somente de áudio porque o sistema de legenda precisa de vídeo para funcionar. Sem vídeo, não há dimensão viewport e, sem uma dimensão viewport, não é possível exibir gráficos para legendas.
* A partir da versão 1.4.23, o TVSDK não oferecerá suporte ao Gingerpão OS 2.3. Isso ocorre porque o TVSDK usou as seguintes bibliotecas privadas do Android para coletar informações de hardware sobre dispositivos com o sistema operacional Gingerpão:

   * `libstagefright.so`
   * `libcutils.so`

Na versão Android N, o Google removeu o acesso a essas bibliotecas privadas. O Gingerbun OS representa atualmente menos de 1% da participação no mercado do sistema operacional Android globalmente, portanto, após a versão 1.4.23, o sistema operacional Gingerpão não será mais suportado pelo TVSDK.
Ao usar a versão 1.4.23 (que inclui suporte para Android N) ou posterior:
* Atualize seus aplicativos para usar a versão 11 do minSdkVersion.
* Se o usuário final estiver executando o OS 2.3, a versão do SDK será inferior à versão minSdkVersion do aplicativo. O sistema aborta a instalação ou atualização do aplicativo.
* Se o usuário final estiver executando uma versão superior ao OS 2.3, o aplicativo será instalado corretamente.

Se você atualizar minSdkVersion:

* Se o usuário final estiver executando o OS 2.3, o aplicativo será instalado, mas a reprodução não funcionará.
Isso se aplica à atualização e à instalação de limpeza.
* Se o usuário final estiver executando um sistema superior ao OS 2.3, o aplicativo será instalado corretamente e o conteúdo será reproduzido corretamente.

**Versão 1.4.22**

* A saída antecipada dos anúncios não funciona com alguns dos anúncios intermediários quando as tags splice-out e splice-in estão muito próximas.

**Versão 1.4.2**

* O rebobinamento em um intervalo de anúncios está fazendo com que o fluxo seja concluído.

O Media Player envia incorretamente MediaPlayerPlayerState.Complete durante a operação de rebobinamento do Trick Play quando atinge um limite de anúncio. O player deve ignorar esse evento no modo de reprodução de truque; caso contrário, o SDK trata o estado corretamente.

**Versão 1.4.0 (1086)**

* PTPLAY-1634 - A mesma tag Assinada tem carimbos de data e hora diferentes em janelas ativas diferentes. Quando as janelas ativas se movem, a mesma tag em cada uma delas deve ter os mesmos carimbos de data e hora. No entanto, às vezes, mesmo as mesmas tags têm carimbos de data e hora diferentes.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE às vezes é visto após vários switches de/para o fluxo alternativo em blecautes
* Erro #3726865 - Se um fluxo LBA de taxa de bits múltipla for start de um fluxo somente de áudio, o vídeo não será exibido se for alternado para um fluxo de áudio/vídeo. Iniciar a partir de um fluxo de Áudio/Vídeo não exibirá esse problema e poderá alternar com êxito entre fluxos de Áudio e Áudio/Vídeo
* Bug #3760144 - A resolução pode mudar ou parecer pulsar quando um fluxo é pausado em alguns dispositivos como Kindle Fire 7 e Samsung Galaxy Nexus. Observável apenas sob inspeção atenta
* Erro #3761170 - o SearchToLocal in Live with Ads não pode procurar novamente no conteúdo do anúncio; é melhor usar as APIs currentTime para fluxos ao vivo
* Bug #3763370 - Os fluxos ao vivo com anúncios exibirão ocasionalmente dois marcadores de anúncio próximos quando deveria haver apenas um. Esses marcadores de anúncio representam o mesmo anúncio, e somente um será reproduzido
* Erro #3763373 - O marcador de anúncio pode desaparecer brevemente ao buscar além de um anúncio em fluxos VOD. O marcador de anúncio é restaurado e não há outro efeito adverso na linha do tempo
* Alguns dispositivos têm problemas conhecidos de reprodução. Para obter mais informações, consulte Problemas de dispositivo [conhecidos na versão 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementação de referência - A reprodução de truque não é implementada no aplicativo de amostra.

## Problemas de dispositivo conhecidos na versão 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Solução |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | Atraso ABR é esperado desde que o decodificador esteja sendo reiniciado. |  |  |
| Desejo HTC (diferente do desejo HTC HD) | QSD8250 | Não é possível reproduzir vídeo. Retorna o erro VIDEO_PERFIL_NOT_SUPPORTED. | O desejo não fornece um decodificador HW adequado. Dá o decodificador SW de Stagefright. | Reinicie o dispositivo. |
| HTC EVO 4G | QSD8650 | Sem decodificador HW. | Qualcomm não tem um decodificador HW. | Atualize para Android 4.x. |
| Kindle FireSystem versão 6.0 | TI OMAP4 | Não joga streams HLS. O vídeo no AIR não funciona. |  | Atualize para a versão 6.3 do sistema. |
| Kindle Fire HD | TI OMAP4 | Pode entrar em um estado em que não pode reproduzir vídeo. Retorna os erros VIDEO_PERFIL_NOT_SUPPORTED e UNRECOVERABLE_ERROR. | O decodificador de hardware fica em um estado irrecuperável quando o aplicativo não encerra totalmente o decodificador de hardware, por exemplo, após encontrar uma falha. Também ocorre em aplicativos nativos no dispositivo. | Reinicie o dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | O AVE trava após vários switches ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemas gerais de desempenho com o AVE em vez do AIR. Áudio/vídeo fora de sincronização, a reprodução congela após reproduzir entre 9 e 15 minutos. Falhas. | Possivelmente relacionado ao openGLES que ativamos no AIR. A ser investigado. |  |
| Nexus 7 (2ª geração) | S4Pro APQ8064 (Qualcomm) | O dispositivo trava quando um filme é pausado por mais de 30 minutos. | Problema de dispositivo que foi reportado ao Google. | O tempo limite do aplicativo deve ser excedido para não permitir um estado de pausa longo. |
| Nexus S (GB) | Pássaro Humming | Não é possível reproduzir nenhum vídeo usando o decodificador de HW. | Não há decodificador HW baseado em Stagefright no Nexus S, portanto, para Android 2.3, estamos usando um decodificador SW. | Atualize para ICS. |
| Nexus S (ICS) | Pássaro Humming | Ocasionalmente, o vídeo treme. | Dados incorretos podem fazer com que o decodificador fique em um estado ruim. | Reinicie o dispositivo. |
| Nook tabletSistema operacional Android: 2,3 | TI OMAP 4 | O vídeo não é reproduzido e o aplicativo trava. | O Stagefright entra em um estado instável após a execução do aplicativo por algumas vezes. Chamadas para mediaplayer::QueryCodecs congela. | Reinicie o dispositivo para redefinir o estado. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Não é possível instalar o aplicativo SampleMediaPlayer. | Usa ARM v6 em vez do chipset ARM v7 mais comum. O FP/AIR não suporta este dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6. | NovaThor U8500 | Não é possível reproduzir vídeo. | Este chipset é um decodificador desconhecido para Android pre-ICS no AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | O desempenho do vídeo não é igual para este dispositivo. | O decodificador de hardware está retornando quadros decodificados com o PTS errado. Parece que o decodificador está usando o tempo de decodificação em vez do tempo de apresentação. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6. | TI OMAP4 | Falha ao iniciar o vídeo. |  | Atualize para Android 2.3.7 ou 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | Intermitentemente, o vídeo congela e somente o áudio é reproduzido e, em seguida, fica sem resposta. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | O vídeo congela. | Investigando. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | A transição MBR pode levar até três segundos. | Como uma correção para falhas de MBR, reiniciamos o decodificador para cada switch de fluxo, que pode levar até três segundos. |  |
| Samsung Galaxy Y |  | Não é possível instalar o aplicativo SampleMediaPlayer. | Usa ARM v6 em vez do chipset ARM v7 mais comum. O FP/AIR não suporta este dispositivo. |  |
| Xoom | Tegra | Alguns quadros são descartados para troca. O decodificador não é reiniciado. | Limitação OMXAL. |  |

## Recursos úteis {#helpful-resources}

* Consulte a documentação completa da ajuda na página Aprendizagem e suporte [da](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
