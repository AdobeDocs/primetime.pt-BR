---
title: Apêndice B "Dicas de depuração"
description: Apêndice B "Dicas de depuração"
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Apêndice B: Dicas de depuração {#appendix-b-debugging-tips}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Limpando dados temporários {#clearing-temporary-data}

A autenticação da Adobe Primetime armazena dados temporários, como cache do navegador, cache de LSOs e cookies. A limpeza de dados temporários é importante para garantir que você obtenha uma tabulação limpa ao testar.

- [Limpar o cache do navegador e os cookies](#clearing-the-browser-cache-and-cookies)
- [Limpando cache de LSOs](#clearing-lsos-cache)\
    

## Limpar o cache do navegador e os cookies {#clearing-the-browser-cache-and-cookies}

Ele é confiável no navegador, mas no Firefox: &quot;Ferramentas&quot; -\> &quot;Limpar Histórico Recente...&quot; -\> Em &quot;Intervalo de tempo para limpar:&quot; selecione &quot;Tudo&quot;; e em &quot;Detalhes&quot;: marque &quot;Cookies&quot; e &quot;Cache&quot; -\> Clique em &quot;Limpar agora&quot;.\
 

## Limpando cache de LSOs {#clearing-lsos-cache}

Acesse o [Ajuda do Flash Player](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

Selecione o ```entitlement.\*``` (dependendo do que está sendo testado) e clique em &quot;Excluir site&quot;.\
 

## Ferramentas de depuração {#tools}

Os engenheiros de autenticação da Adobe Primetime usam as seguintes ferramentas de depuração:

- Firebug - <http://www.getfirebug.com/>
- Flashbug (funciona com a versão de depuração do flash player) <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Cabeçalhos http ao vivo - <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->