---
description: A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.
title: Otimização de redirecionamento HTTP 302
exl-id: 80d5d38d-c998-4fc0-b527-b38e578d76e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Otimização de redirecionamento HTTP 302 {#http-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver habilitada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas 302 adicionais. Esse recurso é ativado por padrão e você pode alterar essa configuração.

>[!IMPORTANT]
>
>Esse recurso é compatível somente com navegadores certificados que oferecem suporte ao `responseURL` propriedade na `XMLHttpRequest` objeto.

Para fallback de Flash, lembre-se das seguintes informações:

* Os usuários finais devem ter o Flash Player Adobe versão 23 ou posterior instalado.
* Se a integridade do fluxo estiver desativada, o redirecionamento 302 será suportado somente em navegadores certificados.

## Desabilitar otimização de redirecionamento 302 {#disabling-redirect-optimization}

Você pode usar a propriedade useRedirectUrl para habilitar o redirecionamento 302 (true) ou a desabilitação (false).

Por exemplo:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
