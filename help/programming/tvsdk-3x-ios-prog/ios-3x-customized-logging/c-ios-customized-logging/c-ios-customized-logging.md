---
description: Você pode implementar seu próprio sistema de registro.
seo-description: Você pode implementar seu próprio sistema de registro.
seo-title: Compreensão do registro personalizado
title: Compreensão do registro personalizado
uuid: f056d7d7-ec3a-4cf1-997f-72a89bbc9447
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Registro personalizado {#customized-logging}

Você pode implementar seu próprio sistema de registro.

Além de fazer logon usando notificações predefinidas, você pode implementar um sistema de registro que usa as mensagens e mensagens de registro geradas pelo TVSDK. Para obter mais informações sobre notificações predefinidas, consulte [O Sistema](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System)de Notificação. Você pode usar esses registros para solucionar problemas nos aplicativos do player e para fornecer uma melhor compreensão do fluxo de trabalho de reprodução e publicidade.

O registro em log personalizado usa uma instância singleton compartilhada do `PSDKPTLogFactory`, que fornece um mecanismo para registrar mensagens em vários loggers. Você define e adiciona (registra) um ou mais registradores ao `PTLogFactory`. Isso permite que você defina vários registradores com implementações personalizadas, como um registrador de console, um registrador da Web ou um registrador de histórico de console.

O TVSDK gera mensagens de log para muitas de suas atividades, que são `PTLogFactory` encaminhadas para todos os registradores. Seu aplicativo também pode gerar mensagens de log personalizadas, que são encaminhadas para todos os registradores. Cada agente de log pode filtrar as mensagens e tomar as medidas apropriadas.

Há duas implementações para `PTLogFactory`:

* Para ouvir registros.
* Para adicionar logs a um `PTLogFactory`.

## Escutar registros {#listen-to-logs}

Para se registrar para escutar registros:
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

1. Para registrar a instância para receber entradas de registro, adicione uma instância do `PTLogger` ao `PTLoggerFactory`:

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

## Adicionar novas mensagens de registro {#add-new-log-messages}

Para se registrar para ouvir os registros:

Crie um novo `PTLogEntry` e adicione-o a `thePTLogFactory`:

É possível instanciar manualmente uma ocorrência `PTLogEntry` e adicioná-la à instância `PTLogFactory` compartilhada ou usar uma das macros para realizar a mesma tarefa.

Este é um exemplo de registro usando a `PTLogDebug` macro:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
