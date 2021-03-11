---
description: Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.
title: Personalizar reprodução com anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# Personalizar reprodução com anúncios{#customize-playback-with-ads}

Quando a reprodução atinge um ad break, passa um ad break ou termina em um ad break, o TVSDK define algum comportamento padrão para o posicionamento do indicador de reprodução atual.

>[!TIP]
>
>Você pode substituir o comportamento padrão usando a classe `PTAdPolicySelector`.

O comportamento padrão varia dependendo se o usuário passa o ad break durante a reprodução normal ou ao buscar em um vídeo.

Você pode personalizar o comportamento da reprodução de anúncio das seguintes maneiras:

* Salve a posição em que o usuário parou de assistir ao vídeo e retomou a reprodução na mesma posição em uma sessão futura.
* Se um ad break for apresentado ao usuário, ele não exibirá anúncios adicionais por alguns minutos, mesmo se o usuário buscar uma nova posição.
* Se o conteúdo não for reproduzido após alguns minutos, reinicie o fluxo ou faça failover para uma fonte diferente para o mesmo conteúdo.

   Na sessão de reprodução de failover, para permitir que o usuário ignore os anúncios e retome para a posição de falha anterior, é possível desativar os anúncios precedentes e/ou intermediários. O TVSDK fornece métodos para permitir a ignorância de anúncios precedentes e intermediários.

## Elementos de API para reprodução de anúncio {#section_296ADE00CFEA40CBA1B46142720D13A5}

O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
Os seguintes elementos da API são úteis para personalizar a reprodução:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento da API </th> 
   <th colname="col2" class="entry"> Conteúdo compatível com publicidade </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata  </span> </td> 
   <td colname="col2"> Controle se um ad break deve ser marcado como visto por um visualizador e, em caso positivo, quando marcá-lo. Defina e obtenha a política assistida usando a propriedade <span class="codeph"> adBreakAsWatched </span> . </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector  </span> </td> 
   <td colname="col2"> Protocolo que permite a personalização do comportamento do anúncio TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> Classe que implementa o comportamento padrão do TVSDK. Seu aplicativo pode substituir essa classe para personalizar os comportamentos padrão sem implementar a interface completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer  </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime  </span>. <p>Esse é o horário local da reprodução, excluindo as quebras de anúncio. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocalTime  </span> . <p>Aqui, a busca ocorre em relação a um horário local no fluxo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.conversionToLocalTime  </span>. <p>A posição virtual na linha do tempo é convertida para a posição local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak  </span> </td> 
   <td colname="col2"> <span class="codeph">  </span> propriedade isWatched Indica se o visualizador assistiu ao anúncio. </td> 
  </tr> 
 </tbody> 
</table>

## Configurar reprodução personalizada {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Antes de personalizar ou substituir comportamentos de publicidade, registre a instância da política de publicidade no TVSDK.

Para personalizar os comportamentos do anúncio, siga um destes procedimentos:

* Siga o protocolo `PTAdPolicySelector` e implemente todos os métodos de seleção de política necessários.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de publicidade padrão.

* Substitua a classe `PTDefaultAdPolicySelector` e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **some** dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

1. Registre a instância de política a ser usada pelo TVSDK por meio da fábrica do cliente.

   >[!NOTE]
   >
   >As políticas de anúncio personalizadas registradas no início da reprodução são apagadas quando a instância `PTMediaPlayer` é desalocada. O aplicativo deve registrar uma instância do seletor de políticas sempre que uma nova sessão de reprodução for criada.

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

Por padrão, o TVSDK força a reprodução de um ad break quando o usuário busca um ad break. Você pode personalizar o comportamento para ignorar um ad break se o tempo decorrido desde o término de um ad break anterior estiver em um determinado número de minutos.

>[!IMPORTANT]
>
>Quando há uma busca interna para ignorar um anúncio, pode haver uma pequena pausa na reprodução.

O exemplo a seguir de um seletor de política de anúncio personalizado ignora os anúncios nos próximos cinco minutos (hora do relógio da parede) depois que o usuário assiste a um ad break.

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

## Salve a posição do vídeo e retome mais tarde {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Você pode salvar a posição atual da reprodução em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

As publicidades inseridas dinamicamente diferem entre sessões de usuário, portanto, salvar a posição **com** publicidades em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição da reprodução ao ignorar anúncios em spliced.

1. Quando o usuário sai de um vídeo, seu aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >As durações dos anúncios não são incluídas.

   As quebras de anúncios podem variar em cada sessão devido aos padrões de anúncios, limite de frequência e assim por diante. O horário atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local . Use a propriedade `localTime` para ler essa posição , que pode ser salva no dispositivo ou em um banco de dados no servidor.

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `currentTime` terá 1200 segundos, enquanto `localTime` nessa posição terá 900 segundos.

   >[!IMPORTANT]
   >
   >A hora local e a hora atual são as mesmas para fluxos ao vivo/lineares. Nesse caso, `convertToLocalTime` não tem efeito. Para VOD, o tempo local permanece inalterado enquanto os anúncios são exibidos.

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

1. Para retomar o vídeo na mesma posição: Para retomar a reprodução do vídeo a partir da posição que foi salva de uma sessão anterior, use `seekToLocalTime`

   >[!TIP]
   >
   >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados de tempo atuais, ocorrerá um comportamento incorreto.

   Para procurar no horário atual, use `seekToTime`.

1. Quando o aplicativo recebe o evento de alteração de status `PTMediaPlayerStatusReady`, procure no horário local salvo.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Forneça os ad breaks conforme especificado na interface da política de anúncios.
1. Implemente um seletor de política de anúncio personalizado estendendo o seletor de política de anúncio padrão.
1. Forneça os ad breaks que devem ser apresentados ao usuário implementando `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Esse método inclui um ad break precedente e o ad breaks intermediários antes da posição de hora local. Seu aplicativo pode decidir reproduzir um ad break precedente e retomar para o horário local especificado, reproduzir um ad break intermediário e retomar para o horário local especificado, ou não reproduzir ad breaks.

