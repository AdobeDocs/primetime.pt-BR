---
description: Quando a reprodução atinge uma pausa de anúncio, passa uma pausa de anúncio ou termina em uma pausa de anúncio, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
seo-description: Quando a reprodução atinge uma pausa de anúncio, passa uma pausa de anúncio ou termina em uma pausa de anúncio, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
seo-title: Personalizar reprodução com anúncios
title: Personalizar reprodução com anúncios
uuid: 58002ec2-65ab-4e3b-8e3b-f755ced5cb5a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Personalizar reprodução com anúncios{#customize-playback-with-ads}

Quando a reprodução atinge uma pausa de anúncio, passa uma pausa de anúncio ou termina em uma pausa de anúncio, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.

>[!TIP]
>
>Você pode substituir o comportamento padrão usando a `PTAdPolicySelector` classe.

O comportamento padrão varia, dependendo se o usuário passa no intervalo do anúncio durante a reprodução normal ou procurando em um vídeo.

Você pode personalizar o comportamento de reprodução de anúncios das seguintes maneiras:

* Salve a posição na qual o usuário parou de assistir ao vídeo e retomará a reprodução na mesma posição em uma sessão futura.
* Se uma pausa de anúncio for apresentada ao usuário, não exiba anúncios adicionais por alguns minutos, mesmo se o usuário buscar uma nova posição.
* Se o conteúdo não for reproduzido após alguns minutos, reinicie o fluxo ou faça failover para uma fonte diferente para o mesmo conteúdo.

   Na sessão de reprodução de failover, para permitir que o usuário pule os anúncios e retome para a posição anterior com falha, você pode desativar os anúncios anteriores e/ou intermediários. O TVSDK fornece métodos para permitir a omissão de anúncios precedentes e intermediários.

## Elementos de API para reprodução de anúncio {#section_296ADE00CFEA40CBA1B46142720D13A5}

O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
Os seguintes elementos de API são úteis para personalizar a reprodução:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento da API </th> 
   <th colname="col2" class="entry"> Conteúdo que suporta publicidade </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> Controle se uma quebra de anúncio deve ser marcada como assistida por um visualizador e, em caso afirmativo, quando marcá-la. Defina e obtenha a política assistida usando a propriedade <span class="codeph"> adBreakAsWatched </span> . </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> Protocolo que permite a personalização do comportamento do anúncio TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe que implementa o comportamento padrão do TVSDK. Seu aplicativo pode substituir essa classe para personalizar os comportamentos padrão sem implementar a interface completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>Esta é a hora local da reprodução, exceto as pausas de anúncio inseridas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocalTime </span> . <p>Aqui, a busca ocorre em relação a uma hora local no fluxo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>A posição virtual na linha do tempo é convertida para a posição local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> propriedade isWatched </span> . Indica se o visualizador assistiu ao anúncio. </td> 
  </tr> 
 </tbody> 
</table>

## Configurar reprodução personalizada {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Antes de personalizar ou substituir comportamentos de publicidade, registre a instância da política de publicidade no TVSDK.

Para personalizar os comportamentos de publicidade, execute um dos procedimentos a seguir:

* Conformar-se ao `PTAdPolicySelector` protocolo e implementar todos os métodos de seleção de política necessários.

   Essa opção é recomendada se você precisar substituir **todos** os comportamentos padrão de anúncio.

* Substitua a `PTDefaultAdPolicySelector` classe e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **alguns** dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

1. Registre a instância de política a ser usada pelo TVSDK na fábrica do cliente.

   >[!NOTE]
   >
   >As políticas de anúncio personalizadas registradas no início da reprodução são apagadas quando a `PTMediaPlayer` instância é desalocada. Seu aplicativo deve registrar uma instância do seletor de política sempre que uma nova sessão de reprodução for criada.

   Por exemplo:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implemente suas personalizações.

## Ignorar quebras de anúncio por um período de tempo {#section_99809BE4D9BB4DEEBBF596C746CA428A}

Por padrão, o TVSDK força uma pausa de anúncio a ser reproduzida quando o usuário busca uma pausa de anúncio. Você pode personalizar o comportamento para ignorar uma quebra de anúncio se o tempo decorrido desde uma conclusão de quebra anterior estiver dentro de um determinado número de minutos.

>[!IMPORTANT]
>
>Quando há uma busca interna para ignorar um anúncio, pode haver uma pequena pausa na reprodução.

O exemplo a seguir de um seletor de política de anúncios personalizado ignora os anúncios nos próximos cinco minutos (hora do relógio da parede) depois que um usuário assistir a uma pausa de anúncio.

1. Registre a instância de política a ser usada pelo TVSDK na fábrica do cliente.

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

## Salve a posição do vídeo e retome mais tarde {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

As publicidades inseridas dinamicamente diferem entre as sessões do usuário, portanto, salvar a posição **com** publicidades em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição de reprodução ao ignorar anúncios segmentados.

1. Quando o usuário sai de um vídeo, seu aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >A duração do anúncio não está incluída.

   As quebras de anúncios podem variar em cada sessão devido aos padrões de anúncios, limitação de frequência e assim por diante. A hora atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local. Use a `localTime` propriedade para ler essa posição, que pode ser salva no dispositivo ou em um banco de dados no servidor.

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `currentTime` terá 1200 segundos, enquanto `localTime` nessa posição serão 900 segundos.

   >[!IMPORTANT]
   >
   >A hora local e a hora atual são as mesmas para fluxos ao vivo/lineares. Neste caso, não `convertToLocalTime` tem efeito. Para VOD, o tempo local permanece inalterado enquanto os anúncios são reproduzidos.

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

1. Para retomar o vídeo na mesma posição: Para retomar a reprodução do vídeo da posição que foi salva de uma sessão anterior, use `seekToLocalTime`

   >[!TIP]
   >
   >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados de tempo atuais, ocorrerá comportamento incorreto.

   Para buscar o horário atual, use `seekToTime`.

1. Quando o aplicativo receber o evento de alteração de `PTMediaPlayerStatusReady` status, procure a hora local salva.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Forneça os intervalos de anúncio conforme especificado na interface da política de anúncios.
1. Implemente um seletor de política de publicidade personalizado estendendo o seletor de política de publicidade padrão.
1. Forneça as pausas de anúncio que devem ser apresentadas ao usuário ao implementar `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Esse método inclui uma pausa de anúncio precedente e uma pausa de anúncio intermediário antes da posição de hora local. Seu aplicativo pode decidir reproduzir um intervalo de anúncios precedente e retomar para o horário local especificado, reproduzir um intervalo de anúncios intermediário e retomar para o horário local especificado, ou não reproduzir nenhum intervalo de anúncios.

