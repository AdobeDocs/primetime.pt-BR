---
description: A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.
title: Desabilitar ou habilitar otimização de redirecionamento 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Otimização de redirecionamento HTTP 302 {#http-302-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver habilitada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas 302 adicionais.

Esse recurso é ativado por padrão e você pode alterar essa configuração.

## Desabilitar ou habilitar otimização de redirecionamento 302{#disable-or-enable-redirect-optimization}

Use o `useRedirectedUrl` para ativar (true) ou desativar (false) o redirecionamento 302.
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
