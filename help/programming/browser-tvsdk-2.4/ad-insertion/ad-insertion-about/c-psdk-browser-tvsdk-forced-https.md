---
description: nulo
seo-description: nulo
seo-title: Carregamento seguro de anúncios em HTTPS
title: Carregamento seguro de anúncios em HTTPS
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Carregamento seguro de anúncios em HTTPS{#secure-ad-loading-over-https}

O Adobe Primetime pode solicitar servidores de anúncios de terceiros em https mesmo se o player estiver hospedado em http. Somente as chamadas de servidores de anúncios são atualizadas para https que o cliente procura durante a fase do resolvedor de anúncios do Auditude.

>[!NOTE]
>
>Este recurso não é compatível com Flash.

Use o seguinte para ativar o carregamento seguro de anúncios. Não está ativado por padrão.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
