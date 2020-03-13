---
description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-title: Desabilitar ou habilitar a otimização de redirecionamento 302
title: Desabilitar ou habilitar a otimização de redirecionamento 302
uuid: 7561839f-aec6-4a59-a07a-7e4fa043fdc2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Otimização de redirecionamento HTTP 302 {#http-302-redirect-optimization}

A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita 302 respostas adicionais.

Esse recurso é ativado por padrão e você pode alterar essa configuração.

## Desabilitar ou habilitar a otimização de redirecionamento 302{#disable-or-enable-redirect-optimization}

Use a `useRedirectedUrl` propriedade para ativar (true) ou desativar (false) o redirecionamento 302.
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

