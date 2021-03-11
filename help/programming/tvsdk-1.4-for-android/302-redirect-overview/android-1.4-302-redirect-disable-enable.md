---
description: A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.
title: Desative ou ative a otimização de redirecionamento 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---


# Otimização de redirecionamento HTTP 302 {#http-302-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no reprodutor, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas adicionais 302.

Esse recurso é ativado por padrão e você pode alterar essa configuração.

## Desative ou ative a otimização de redirecionamento 302{#disable-or-enable-redirect-optimization}

Use a propriedade `useRedirectedUrl` para ativar ou desativar o redirecionamento 302 (true).
Por exemplo:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```

