---
description: Você pode implementar seu próprio sistema de registro.
title: Como entender o registro personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Registro personalizado {#customized-logging}

Você pode implementar seu próprio sistema de registro.

Além de fazer logon usando notificações predefinidas, é possível implementar um sistema de registro que use mensagens e mensagens de log geradas pelo TVSDK. Para obter mais informações sobre notificações predefinidas, consulte [O Sistema de Notificação](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System). Você pode usar esses registros para solucionar problemas de aplicativos do player e fornecer uma melhor compreensão do fluxo de trabalho de reprodução e publicidade.

O registro personalizado usa uma instância singleton compartilhada do `PSDKPTLogFactory`, que fornece um mecanismo para registrar mensagens em vários loggers. Você define e adiciona (registre) um ou mais registradores ao `PTLogFactory`. Isso permite definir vários loggers com implementações personalizadas, como um logger do console, um logger da Web ou um logger do histórico do console.

O TVSDK gera mensagens de log para muitas de suas atividades, que o `PTLogFactory` encaminha para todos os registradores. Seu aplicativo também pode gerar mensagens de log personalizadas, que são encaminhadas para todos os registradores registrados. Cada logger pode filtrar as mensagens e tomar as medidas apropriadas.

Há duas implementações para `PTLogFactory`:

* Para acompanhamento de logs.
* Para adicionar logs a um `PTLogFactory`.

## Escute os logs {#listen-to-logs}

Para se registrar para escutar logs:
1. Implemente uma classe personalizada que siga o protocolo `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. Para registrar a instância para receber entradas de log, adicione uma instância do `PTLogger` ao `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Este é um exemplo de logs de filtragem usando o tipo `PTLogEntry` :

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## Adicionar novas mensagens de log {#add-new-log-messages}

Para registrar-se para escutar os logs:

Crie um novo `PTLogEntry` e adicione-o a `thePTLogFactory`:

Você pode instanciar manualmente um `PTLogEntry` e adicioná-lo à instância compartilhada `PTLogFactory` ou usar uma das macros para realizar a mesma tarefa.

Este é um exemplo de registro usando a macro `PTLogDebug`:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
