---
description: Você pode implementar seu próprio sistema de registro.
title: Registro personalizado
exl-id: 7e10e2bd-24cc-4fe7-ad95-d466cb4baa42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Registro personalizado {#customized-logging}

Você pode implementar seu próprio sistema de registro.

Além de fazer logon usando notificações predefinidas, você pode implementar um sistema de log que use as mensagens de log e as mensagens geradas pelo TVSDK. Para obter mais informações sobre notificações predefinidas, consulte [O sistema de notificação](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). Você pode usar esses registros para solucionar problemas nos aplicativos do player e fornecer uma melhor compreensão do fluxo de trabalho de reprodução e publicidade.

O log personalizado usa uma instância singleton compartilhada do `PSDKPTLogFactory`, que fornece um mecanismo para registrar mensagens em vários registradores. Você define e adiciona (registra) um ou mais registradores à `PTLogFactory`. Isso permite definir vários registradores com implementações personalizadas, como um registrador de console, um registrador da Web ou um registrador de histórico de console.

O TVSDK gera mensagens de log para muitas de suas atividades, que o `PTLogFactory` encaminha para todos os registrados. Seu aplicativo também pode gerar mensagens de log personalizadas, que são encaminhadas a todos os logs registrados. Cada agente de log pode filtrar as mensagens e tomar as medidas apropriadas.

Há duas implementações para `PTLogFactory`:

* Para ouvir logs.
* Para adicionar logs a um `PTLogFactory`.

## Ouvir logs {#listen-to-logs}

Para registrar-se para ouvir logs:
1. Implementar uma classe personalizada que siga o protocolo `PTLogger`:

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

1. Para registrar a instância para receber entradas de log, adicione uma instância da `PTLogger` para o `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Este é um exemplo de filtragem de logs usando o `PTLogEntry` tipo:

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

Para registrar-se para acompanhar logs:
1. Criar um novo `PTLogEntry` e adicioná-lo a `thePTLogFactory`:

   É possível instanciar manualmente um `PTLogEntry` e adicione-o à `PTLogFactory` instância compartilhada ou use uma das macros para realizar a mesma tarefa.

   Este é um exemplo de registro usando o `PTLogDebug` macro:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
