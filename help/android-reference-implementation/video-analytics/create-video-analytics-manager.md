---
description: Criar o Video Analytics Manager
seo-description: Criar o Video Analytics Manager
seo-title: Criar o Video Analytics Manager
title: Criar o Video Analytics Manager
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Criar o Video Analytics Manager {#create-the-video-analytics-manager}

Uma nova classe de gerente ( `VAManager`) foi adicionada à Implementação de referência do Android. `VAManager` simplesmente cria e destrói uma instância da `VideoHeartbeat` classe. A implementação de referência cria uma `VAManager` instância quando uma nova `MediaPlayer` é criada e destrói essa instância quando a `MediaPlayer` é destruída. Isso é implementado em `PlayerFragment.java`.

## Para criar um novo Video Analytics Manager

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

A variável de configuração é uma implementação concreta de `IVAConfig` e contém as `VideoHeartbeat` configurações de tempo de execução.

>[!NOTE]
>
>Se o aplicativo Android não estiver configurado com uma conta do Adobe Analytics, os dados de rastreamento de vídeo não serão gerados, mesmo se uma instância do `VAManager` for criada e ativada.

