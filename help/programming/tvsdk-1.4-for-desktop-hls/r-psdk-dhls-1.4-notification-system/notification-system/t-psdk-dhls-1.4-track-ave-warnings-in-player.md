---
description: Usando o NotificationEvent, você pode rastrear avisos transmitidos pelo Mecanismo de vídeo Adobe (AVE).
seo-description: Usando o NotificationEvent, você pode rastrear avisos transmitidos pelo Mecanismo de vídeo Adobe (AVE).
seo-title: Rastrear avisos AVE em seu player
title: Rastrear avisos AVE em seu player
uuid: 236aee5e-6b1a-4298-9d3b-f33b40416c19
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# Rastrear avisos AVE em seu player{#track-ave-warnings-in-your-player}

Usando o NotificationEvent, você pode rastrear avisos transmitidos pelo Mecanismo de vídeo Adobe (AVE).

O aplicativo do player pode rastrear avisos e erros de reprodução gerados pelo AVE, como eventos de failover ou de rede desativados que não interrompem a reprodução e não exigem necessariamente nenhuma ação do aplicativo. Embora alguns erros de AVE sejam tratados pelo TVSDK, `NotificationEvent` serve como um mecanismo de passagem geral para a camada do aplicativo para avisos de AVE. Depois de receber avisos AVE, você pode optar por realizar alguma ação, como interromper a reprodução de forma proativa, ativar um plano de contingência, registrar mensagens e assim por diante.

Use os seguintes elementos de API para rastrear avisos AVE no player:

**NotificationCode**

```
public final class NotificationCode { 
    /** 
     * Warning message for playback status. 
     */ 
    public static const GENERAL_WARNING:int = 101100; 
}
```

**NotificationEvent**

```
/** 
 * Event dispatched by MediaPlayer when a notification is available 
 * for the current media stream being played. 
 */ 
public class NotificationEvent extends Event { 
    /** 
     * Event dispatched when a new warning has been received for the current item. 
     * 
     * The newly created Notification object can be accessed through  
     * the notification property of this event. 
     */ 
    public static const WARNING_AVAILABLE:String = "warningAvailable"; 
    /** 
     * Helper method for creating NotificationEvent events. 
     * Throws an ArgumentError if the specified ad break is null. 
     * @param notification Associated notification object. 
     * 
     * @return a valid notification event instance. 
     */ 
    public static function create( 
           type:String, notification:Notification):NotificationEvent; 
     /** 
     * Default constructor 
     * Throws an ArgumentError if the specified ad break is null. 
     * @param type           Event type. 
     * @param bubbles        Whether the event can bubble up the display list hierarchy. 
     * @param cancelable     Whether the behavior associated with the event can be prevented. 
     * @param notification   Associated notification object. 
     */ 
    public function NotificationEvent(type:String,  
                                      bubbles:Boolean=false,  
                                      cancelable:Boolean=false,  
                                      notification:Notification= null); 
     /** 
     * The notification associated with this event. 
     */ 
    public function get notification():Notification; 
    /** 
     * @inheritDoc 
     */ 
    public override function clone():Event; 
}
```

Adicione um ouvinte de evento ao player para receber avisos AVE.

Por exemplo:

```
var _player:DefaultMediaPlayer = new DefaultMediaPlayer(context); 
_player.addEventListener(NotificationEvent.WARNING_AVAILABLE, onWarningAvailable); 
 
private function onWarningAvailable(event:NotificationEvent):void { 
    var metadata:Metadata = event.notification.metadata; 
    if (metadata != null) { 
        for each (var key:String in metadata.keySet()) { 
            var value:String = metadata.getValue(key); 
            if (!StringUtils.isEmpty(key) && !StringUtils.isEmpty(value)) { 
                _logger.warn("#onWarningAvailable metadata [{0}:{1}]", key, value); 
            } 
        } 
    } 
} 
```

<!--<a id="example_C35262605D394718B40C084B569A5052"></a>-->

Este é um exemplo de avisos AVE que foram rastreados usando `NotificationEvent`:

```
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [resourceType:HLS] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [resourceId:0] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [runtimeCode:66] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [runtimeCodeMessage:SEGMENT_SKIPPED_ON_FAILURE] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [eventType:Warning] 
 
<pre>
  [WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [description:url::= 
   https://xyz.corp.adobe.com/pmp/assets/abc/failover/tc.1.04/content/backup-01/ 
   low-res/main-stream4-4x3-info6.ts,periodIndex::=0, 
   sizeBytes::=0,downloadTime(ms)::=0,mediaDuration(ms)::=0] 
</pre>
```
