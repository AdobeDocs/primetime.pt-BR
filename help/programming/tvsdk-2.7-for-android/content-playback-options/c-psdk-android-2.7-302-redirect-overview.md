---
description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-title: Otimização de redirecionamento HTTP 302
title: Otimização de redirecionamento HTTP 302
uuid: 4bee0555-ae46-47c1-a067-206ad7ca8883
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Otimização de redirecionamento HTTP 302 {#http-redirect-optimization}

A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita 302 respostas adicionais. Esse recurso é ativado por padrão e você pode alterar essa configuração.

## Desabilitar ou habilitar a otimização de redirecionamento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Use a `useRedirectedUrl` propriedade para ativar ou desativar o redirecionamento 302 ( `true`) ou `false`).

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

Por exemplo:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```

