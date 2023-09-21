---
description: Criar o Gerenciador de análise de vídeo
title: Criar o Gerenciador de análise de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Criar o Gerenciador de análise de vídeo {#create-the-video-analytics-manager}

Uma nova classe de gerentes ( `VAManager`) foi adicionado à Implementação de referência do Android. `VAManager` O simplesmente cria e destrói uma instância do `VideoHeartbeat` classe. A implementação de referência cria uma `VAManager` instância quando um novo `MediaPlayer` é criada e destrói essa instância quando a variável `MediaPlayer` é destruído. Isso é implementado em `PlayerFragment.java`.

## Para criar um novo Gerenciador de análise de vídeo

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

A variável de configuração é uma implementação concreta do `IVAConfig` e contém o tempo de execução `VideoHeartbeat` configurações.

>[!NOTE]
>
>Se o aplicativo Android não estiver configurado com uma conta Adobe Analytics, os dados de rastreamento de vídeo não serão gerados, mesmo se uma instância de `VAManager` é criado e ativado.
