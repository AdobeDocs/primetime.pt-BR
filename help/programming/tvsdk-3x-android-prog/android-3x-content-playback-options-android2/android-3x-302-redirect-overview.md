---
description: A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.
title: Otimização de redirecionamento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# Otimização de redirecionamento HTTP 302 {#http-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no reprodutor, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas adicionais 302. Esse recurso é ativado por padrão e você pode alterar essa configuração.

## Desative ou ative a otimização de redirecionamento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Use a propriedade `useRedirectedUrl` para ativar ou desativar o redirecionamento 302 ( `true`) ou ( `false`).

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
