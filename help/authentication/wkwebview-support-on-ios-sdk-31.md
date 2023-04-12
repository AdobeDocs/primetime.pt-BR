---
title: Suporte a WKWebView no iOS SDK 3.1+
description: Suporte a WKWebView no iOS SDK 3.1+
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Suporte a WKWebView no iOS SDK 3.1+ {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

**Devido à desaprovação do UIWebView do Apple no iOS, atualizamos o SDK 3.1 do iOS com suporte para WKWebView.**

## Compatibilidade {#compatibility}

A partir do iOS SDK versão 3.1, os implementadores podem usar agora WKWebView ou UIWebView alternadamente. Como UIWebView foi descontinuada pelo Apple, os aplicativos devem migrar para WKWebView, para evitar problemas com versões futuras do iOS.

Observe que a migração simplesmente alternaria a classe UIWebView com WKWebView, não há trabalho específico a ser feito em relação ao Adobe implicaria o AccessEnabler.

## Problemas conhecidos {#known-issues}

AdobeEnabler usa uma instância UIWView interna oculta para executar[autenticação passiva](/help/authentication/sso-passive-authn.md)&quot; para certos MVPDs. O fluxo &quot;passivo&quot; foi útil para MVPDs que exigem autenticação para cada id de solicitante e, a partir desse fluxo, beneficiou os Programadores que usaram a mesma id de equipe em vários aplicativos iOS para simular uma experiência SSO (Adobe SSO). Este recurso é atualmente usado por um número limitado de MVPDs.

O recurso usava um comportamento da UIWebView que permitia que o Adobe capturasse os cookies de autenticação e os repetisse durante o fluxo &quot;passivo&quot;. O WKWebView introduz uma segurança mais forte que impede o Adobe de capturar os cookies definidos no logon e repeti-los usando uma instância oculta do WKWebView. Devido a essa melhoria na segurança e considerando que o fluxo &quot;passivo&quot; beneficiou apenas um conjunto muito limitado de MVPDs em um cenário de implementação muito específico (vários aplicativos usando a mesma id de equipe), o Adobe removeu o recurso de &quot;autenticação passiva&quot; para MVPDs usando webviews para autenticação.

O recurso ainda está presente para MVPDs configuradas para usar SFSafariViewController, mas observe que, nesse caso, a autenticação &quot;passiva&quot; estará visível para o usuário, pois SFSafariViewController não pode ser usado de forma &quot;oculta&quot;.
