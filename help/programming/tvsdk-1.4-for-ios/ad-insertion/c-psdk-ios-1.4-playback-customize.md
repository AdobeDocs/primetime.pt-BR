---
description: Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
title: Personalizar reprodução com anúncios
exl-id: f59e94c2-7ca0-4e0b-b0b1-af076fdd4064
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# Personalizar reprodução com anúncios{#customize-playback-with-ads}

Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.

>[!TIP]
>
>Você pode substituir o comportamento padrão usando o `PTAdPolicySelector` classe.

O comportamento padrão varia, dependendo se o usuário passa o ad break durante a reprodução normal ou procurando em um vídeo.

Você pode personalizar o comportamento de reprodução das seguintes maneiras:

* Salve a posição em que o usuário parou de assistir ao vídeo e retome a reprodução na mesma posição em uma sessão futura.
* Se um ad break for apresentado ao usuário, ele não exibirá anúncios adicionais por alguns minutos, mesmo se o usuário buscar uma nova posição.
* Se o conteúdo não for reproduzido após alguns minutos, reinicie o fluxo ou faça failover para uma origem diferente para o mesmo conteúdo.

   Na sessão de reprodução de failover, para permitir que o usuário ignore os anúncios e retome para a posição de falha anterior, é possível desativar os anúncios precedentes e/ou intermediários. O TVSDK fornece métodos para permitir ignorar anúncios precedentes e intermediários.

## Elementos da API para reprodução de anúncio {#section_296ADE00CFEA40CBA1B46142720D13A5}

O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
Os seguintes elementos de API são úteis para personalizar a reprodução:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento de API </th> 
   <th colname="col2" class="entry"> Conteúdo que suporta publicidade </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> Controla se um ad break deve ser marcado como tendo sido assistido por um visualizador e, em caso afirmativo, quando marcá-lo. Definir e obter a política observada usando <span class="codeph"> adBreakAsWatched </span> propriedade. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> Protocolo que permite a personalização do comportamento de anúncio do TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe que implementa o comportamento padrão do TVSDK. Seu aplicativo pode substituir essa classe para personalizar os comportamentos padrão sem implementar a interface completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>Essa é a hora local da reprodução, exceto os ad breaks colocados. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>Aqui, a busca ocorre em relação a uma hora local no fluxo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>A posição virtual na linha do tempo é convertida na posição local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdbreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> propriedade. Indica se o visualizador assistiu ao anúncio. </td> 
  </tr> 
 </tbody> 
</table>

## Configurar reprodução personalizada {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Antes de personalizar ou substituir comportamentos de anúncios, registre a instância da política de anúncios com o TVSDK.

Para personalizar comportamentos de anúncios, siga um destes procedimentos:

* Conformidade com o `PTAdPolicySelector` e implementar todos os métodos de seleção de políticas necessários.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de anúncio padrão.

* Substituir o `PTDefaultAdPolicySelector` e fornecem implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas o **alguns** dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

1. Registre a instância de política a ser usada pelo TVSDK por meio da fábrica do cliente.

   >[!NOTE]
   >
   >As políticas de anúncios personalizados registradas no início da reprodução são apagadas quando a variável `PTMediaPlayer` instância desalocada. Seu aplicativo deve registrar uma instância do seletor de políticas sempre que uma nova sessão de reprodução for criada.

   Por exemplo:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implemente suas personalizações.

## Ignorar ad breaks por um período {#section_99809BE4D9BB4DEEBBF596C746CA428A}

Por padrão, o TVSDK força um ad break a ser reproduzido quando o usuário busca um ad break. Você pode personalizar o comportamento para ignorar um intervalo comercial se o tempo decorrido desde a conclusão de um intervalo anterior estiver dentro de um determinado número de minutos.

>[!IMPORTANT]
>
>Quando há uma busca interna para ignorar um anúncio, pode haver uma pequena pausa na reprodução.

O exemplo a seguir de um seletor de política de anúncio personalizado ignora anúncios nos próximos cinco minutos (tempo do relógio de parede) depois que um usuário assiste a um ad break.

1. Registre a instância de política a ser usada pelo TVSDK por meio da fábrica do cliente.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implemente sua personalização.

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## Salvar a posição do vídeo e retomar mais tarde {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

Os anúncios inseridos dinamicamente diferem entre as sessões do usuário, portanto, salvar a posição **com** anúncios em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição de reprodução, ignorando anúncios empacotados.

1. Quando o usuário sai de um vídeo, o aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >A duração do anúncio não está incluída.

   Os ad breaks podem variar em cada sessão devido a padrões de anúncios, limite de frequência e assim por diante. A hora atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local . Use o  `localTime` para ler esta posição, que pode ser salva no dispositivo ou em um banco de dados no servidor.

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `currentTime` será de 1200 segundos, enquanto `localTime` nesta posição serão 900 segundos.

   >[!IMPORTANT]
   >
   >A hora local e a hora atual são as mesmas para fluxos ao vivo/lineares. Nesse caso, `convertToLocalTime` não tem efeito. Para VOD, a hora local permanece inalterada durante a reprodução dos anúncios.

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. Para retomar o vídeo na mesma posição: Para retomar a reprodução do vídeo a partir da posição salva em uma sessão anterior, use `seekToLocalTime`

   >[!TIP]
   >
   >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados da hora atual, ocorrerá um comportamento incorreto.

   Para buscar o horário atual, use `seekToTime`.

1. Quando o aplicativo recebe a variável `PTMediaPlayerStatusReady` evento de alteração de status, procure a hora local salva.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Forneça os ad breaks de acordo com as especificações da interface de política de anúncios.
1. Implemente um seletor de política de anúncios personalizado estendendo o seletor de política de anúncios padrão.
1. Fornecer os ad breaks que devem ser apresentados ao usuário implementando `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Esse método inclui um ad break precedente e ad breaks intermediários antes da posição da hora local. Seu aplicativo pode decidir reproduzir um ad break precedente e retomar o horário local especificado, reproduzir um ad break intermediário e retomar o horário local especificado ou não reproduzir ad breaks.
