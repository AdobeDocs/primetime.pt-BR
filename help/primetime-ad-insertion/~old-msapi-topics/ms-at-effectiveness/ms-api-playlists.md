---
description: O servidor manifest retorna listas de reprodução principais no formato M3U8, em conformidade com o padrão HTTP Live Streaming proposto. Ele consiste em um conjunto de fluxos de transporte de variante (TSs), cada um contendo representações do mesmo conteúdo para diferentes formatos e taxas de bits. A inserção de anúncio do Adobe Primetime adiciona a tag da diretiva EXT-X-MARKER, que deve ser interpretada pelos players de vídeo do cliente.
title: Diretiva EXT-X-MARKER
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# Diretiva EXT-X-MARKER {#ext-x-marker-directive}

O servidor manifest retorna listas de reprodução principais no formato M3U8, em conformidade com o padrão HTTP Live Streaming proposto. Ele consiste em um conjunto de fluxos de transporte de variante (TSs), cada um contendo representações do mesmo conteúdo para diferentes formatos e taxas de bits. A inserção de anúncio do Adobe Primetime adiciona a tag da diretiva EXT-X-MARKER, que deve ser interpretada pelos players de vídeo do cliente.

Para obter detalhes sobre a tag EXT-X-MARKER, consulte [Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Essa funcionalidade só estará disponível se o URL do servidor de manifesto do bootstrap não contiver o parâmetro `pttrackingmode`.

>[!NOTE]
>
>A tag EXT-X-MARKER é adicionada a segmentos de publicidade e não a segmentos de conteúdo.

O padrão de rascunho em [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) descreve o conteúdo e o formato das listas de reprodução de variante. A tag EXT-X-MARKER direciona o cliente para chamar um retorno de chamada. Ele contém os seguintes componentes:

* **** Identificador exclusivo (cadeia de caracteres) para este evento de retorno de chamada no contexto do fluxo do programa.

* **** TYPEType (cadeia de caracteres) do evento de retorno de chamada: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd ou AdBegin

* **** DURATIONLength de tempo (em segundos) a partir do início do segmento que transporta a tag para a qual a diretiva permanece válida.

* **** OFFSETOptional. O deslocamento (em segundos) relativo ao início da reprodução do segmento, quando a chamada de retorno deve ser invocada.

   * `PodBegin` e  `PrerollPodBegin` contêm informações de beacon no atributo DATA e são acionadas no início do segmento. Portanto, a tag `OFFSET` não está disponível aqui.

   * `AdBegin` contém informações de beacon no atributo DATA e as tags de impressão são acionadas no início desse segmento. Portanto, a tag `OFFSET` também não está disponível aqui.

   * `PodEnd` e  `PrerollPodEnd` contêm informações de beacon no atributo DATA , mas são acionadas no final do segmento atual, pois espera-se que essas tags sejam acionadas no final do último segmento do último anúncio no pod. Nesse caso, `OFFSET` é definido como `<duration of segment>` para especificar que o beacon seja acionado no final do segmento atual.

* **** Sequência de caracteres codificada em DATABase64 entre aspas duplas contendo os dados a serem passados para o aplicativo ao chamar o retorno de chamada. Ele contém informações de rastreamento de anúncios que estão em conformidade com as especificações VMAP1.0 e VAST3.0.

* **** CONTAGEM de anúncios que serão compilados no ad break.

   Aplicável somente se o componente TYPE estiver definido como PodBegin ou PrerollPodBegin.

* **** DETALHAMENTO Duração total (em segundos) do ad break preenchido.

   Aplicável somente se o componente TYPE estiver definido como PodBegin ou PrerollPodBegin.

Ao construir o retorno de chamada, interprete os componentes EXT-X-MARKER da seguinte maneira:

* Quando a tag contiver `OFFSET`, acione o retorno de chamada no deslocamento especificado em relação ao início da reprodução do conteúdo nesse segmento. Caso contrário, acione o retorno de chamada assim que o conteúdo desse segmento começar a ser reproduzido.
* Use `DURATION` para rastrear o progresso do conteúdo do anúncio e solicitar URLs para eventos de rastreamento.
* Passe `ID`, `TYPE` e `DATA` para o retorno de chamada.

Use os valores `PrerollPodBegin` e `PrerollPodEnd` para `TYPE` para decidir qual segmento TS reproduzir primeiro em fluxos ao vivo/lineares.

>[!NOTE]
>
>Os valores `PrerollPodBegin` e `PrerollPodEnd` só estão disponíveis quando um anúncio precedente é inserido em um stream ao vivo.

O servidor de manifesto inclui tags EXT-X-MARKER nos seguintes segmentos:

* O primeiro segmento no ad break, para rastrear o início de um pod de anúncios.
* O primeiro segmento do anúncio, para rastrear o início/conclusão/progresso de um anúncio individual em um pod de anúncio.
* O último segmento no ad break, para rastrear o final de um pod de anúncio.

O servidor manifest envia um documento XML `VMAP1.0-conformant` para rastrear o início e o fim de cada ad break. É uma versão filtrada da resposta VMAP1.0 real retornada pelo servidor de publicidade e contém principalmente os eventos de rastreamento, como mostrado aqui:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

Para cada anúncio que o servidor manifest insere no conteúdo do programa, ele envia um documento XML compatível com o VAST3.0 para rastrear esse anúncio. Cada documento XML contém um elemento `<InLine>` descrevendo o anúncio linear e o anúncio inserido, ou um elemento `<Wrapper>` no caso de anúncios wrapper (ou seja, anúncios vinculados ou redirecionados) e quaisquer anúncios e extensões companheiros associados. Se a resposta VAST contiver um atributo de sequência, como quando o anúncio fizer parte de um pod de anúncio, o documento incluirá esse atributo. Este é um exemplo de documento XML compatível com VAST3.0 para rastrear um anúncio individual:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
