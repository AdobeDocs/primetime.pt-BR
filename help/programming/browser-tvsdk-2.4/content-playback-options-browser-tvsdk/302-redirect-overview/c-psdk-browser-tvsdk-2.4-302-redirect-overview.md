---
description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-title: Otimização de redirecionamento HTTP 302
title: Otimização de redirecionamento HTTP 302
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Otimização de redirecionamento HTTP 302 {#http-redirect-optimization}

A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita 302 respostas adicionais. Esse recurso é ativado por padrão e você pode alterar essa configuração.

>[!IMPORTANT]
>
>Esse recurso é suportado somente nos navegadores certificados que oferecem suporte à propriedade `responseURL` no objeto `XMLHttpRequest`.

Para o fallback do Flash, lembre-se das seguintes informações:

* Seus usuários finais devem ter o Adobe Flash Player versão 23 ou posterior instalado.
* Se a integridade do fluxo estiver desativada, o redirecionamento 302 será suportado somente em navegadores certificados.

## Desabilitando a otimização de redirecionamento 302 {#disabling-redirect-optimization}

Você pode usar a propriedade useRedirectUrl para ativar o redirecionamento 302 (true) ou desativar (false).

Por exemplo:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
