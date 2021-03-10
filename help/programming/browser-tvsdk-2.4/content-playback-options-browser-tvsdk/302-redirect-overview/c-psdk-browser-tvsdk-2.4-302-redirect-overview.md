---
description: A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.
title: Otimização de redirecionamento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Otimização de redirecionamento HTTP 302 {#http-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no reprodutor, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas adicionais 302. Esse recurso é ativado por padrão e você pode alterar essa configuração.

>[!IMPORTANT]
>
>Esse recurso é compatível somente nos navegadores certificados que oferecem suporte à propriedade `responseURL` no objeto `XMLHttpRequest`.

Para fallback de Flash, lembre-se das seguintes informações:

* Seus usuários finais devem ter o Adobe Flash Player versão 23 ou posterior instalado.
* Se a integridade do fluxo estiver desativada, o redirecionamento 302 será suportado apenas em navegadores certificados.

## Desativar a otimização de redirecionamento 302 {#disabling-redirect-optimization}

Você pode usar a propriedade useRedirectUrl para ativar o redirecionamento 302 (true) ou desativar (false).

Por exemplo:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
