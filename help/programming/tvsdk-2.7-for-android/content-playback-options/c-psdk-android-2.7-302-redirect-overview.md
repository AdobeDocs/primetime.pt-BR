---
description: A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.
title: Otimização de redirecionamento HTTP 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Otimização de redirecionamento HTTP 302 {#http-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver habilitada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas 302 adicionais. Esse recurso é ativado por padrão e você pode alterar essa configuração.

## Desabilitar ou habilitar otimização de redirecionamento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Use o `useRedirectedUrl` propriedade para ativar o redirecionamento 302 ( `true`) ou desativado ( `false`).

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
