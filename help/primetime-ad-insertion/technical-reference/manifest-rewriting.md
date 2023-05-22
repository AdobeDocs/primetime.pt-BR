---
title: Regras de regravação e busca de anúncios do manifesto
description: Regras de regravação e busca de anúncios do manifesto
exl-id: 3750abc1-da60-4faf-ba85-37914f33641f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Regras de regravação e busca de anúncios do manifesto {#manifest-rewriting}

O Primetime Ad Insertion é capaz de regravar fragmentos e buscar ativos usando regras simples de pesquisa/substituição.  Isso pode ser usado para converter manualmente https em solicitações http, o que aumentaria o desempenho removendo handshakes de TLS.  Isso também pode ser usado para fornecer ativos de anúncios e cdn da mesma CDN.

As regras são definidas como pesquisa/substituição de expressão regular e podem ser usadas para transformar URLs antes de serem enviadas, bem como depois de inseridas em um manifesto.

Essa regra de exemplo fará a conversão de todas as solicitações de anúncios em domain.com de https para http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

A regra a seguir usará o CDN de conteúdo para fornecer anúncios localizados no CDN de armazenamento de anúncio do Adobe.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

As regras podem ser nomeadas e ativadas/desativadas modificando o `ptprotoswitch` na API do Bootstrap, que é uma lista separada por vírgulas de regras a serem executadas.  Por exemplo, essas duas regras podem ser executadas configurando `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

Entre em contato com o suporte técnico para criar/habilitar essas regras para sua conta.
