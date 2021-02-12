---
title: Regras de regravação de manifesto e busca de anúncios
description: 'Regras de regravação de manifesto e busca de anúncios '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Regras de regravação de manifesto e busca de anúncios {#manifest-rewriting}

O Primetime Ad Insertion é capaz de regravar fragmentos e buscar ativos usando regras simples de pesquisa/substituição.  Isso pode ser usado para converter https para solicitações http, o que aumentaria o desempenho ao remover handshakes TLS.  Isso também pode ser usado para fornecer ativos de anúncio e ativos cdn do mesmo CDN.

As regras são definidas como pesquisa/substituição de expressão regular e podem ser usadas para transformar urls antes de serem enviadas, bem como depois de inseridas em um manifesto.

Esta regra de exemplo fará a conversão de todas as solicitações de anúncio para domain.com de https para http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

A regra a seguir usará o conteúdo CDN para fornecer anúncios localizados no CDN do armazenamento do Adobe.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

As regras podem ser nomeadas e ativadas/desativadas modificando o parâmetro `ptprotoswitch` na API do Bootstrap, que é uma lista de regras para execução separada por vírgulas.  Por exemplo, essas duas regras podem ser executadas ao configurar `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

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

Entre em contato com o suporte técnico para criar/ativar essas regras para a sua conta.