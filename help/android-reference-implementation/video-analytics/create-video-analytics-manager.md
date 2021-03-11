---
description: Criar o Gerenciador de análise de vídeo
title: Criar o Gerenciador de análise de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Crie o Gerenciador do Video Analytics {#create-the-video-analytics-manager}

Uma nova classe de gerente ( `VAManager`) foi adicionada à Implementação de referência do Android. `VAManager` O simplesmente cria e destrói uma instância da  `VideoHeartbeat` classe. A implementação de referência cria uma instância `VAManager` quando um novo `MediaPlayer` é criado e destrói essa instância quando o `MediaPlayer` é destruído. Isso é implementado em `PlayerFragment.java`.

## Para criar um novo Gerenciador do Video Analytics

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

A variável de configuração é uma implementação concreta de `IVAConfig` e contém as configurações de tempo de execução `VideoHeartbeat`.

>[!NOTE]
>
>Se o aplicativo Android não estiver configurado com uma conta Adobe Analytics, os dados de rastreamento de vídeo não serão gerados, mesmo se uma instância de `VAManager` for criada e ativada.

