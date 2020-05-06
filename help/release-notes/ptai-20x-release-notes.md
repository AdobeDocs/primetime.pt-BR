---
title: Notas de versão do PTAI 20.3.3
description: As notas de versão PTAI 20.5.1 descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos na inserção do anúncio dinâmico Primetime no ano 2020.
translation-type: tm+mt
source-git-commit: 2a5866be64895ba13994720bf943dc676c2595bf
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Notas de versão do Primetime Dynamic Ad Insertion 20.5.1

As notas de versão do Dynamic Ad Insertion 20.5.1 descrevem o que é novo ou alterado, os problemas resolvidos e os problemas conhecidos no Primetime Dynamic Ad Insertion no ano 2020.

## Novidades do PTAI 20.5.1

**Quando:** terça-feira, 5 de maio de 2020, das 04:00 às 05:00

* Correção de um problema para garantir que os cabeçalhos CORS corretos fossem fornecidos quando os cabeçalhos If-Modifique-Since fossem enviados.

* Correções de erros no painel CRS.

* Atualizações de manutenção.

## O que mudou em versões anteriores

### Versão 20.3.4

**Quando:** quarta-feira, 1 de abril de 2020, das 03:00 às 04:00

* Corrigido um problema que fazia com que as legendas ficassem fora de sincronização após a inserção do anúncio no VOD/WebVTT.

* Atualizações de segurança.

### Versão 20.3.3

**Quando:** quinta-feira, 26 de março de 2020, das 03h00 às 04h00 do ORIENTE

* As respostas SSAI 4XX e 5XX agora fornecem corretamente cabeçalhos relacionados ao CORS, permitindo que clientes javascript/webview entre domínios leiam com êxito respostas de erro.

* Correção de um problema com cabeçalhos X-Forwarded-For, em que os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Correção de um problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentavam incorretamente.

### Versão 20.1.3

**Quando:** terça-feira, 28 de janeiro de 2020, das 2h00 às 03h00 no leste

* **VMAP com suporte a FER para CueFormat** Converter dicas do fluxo de FER em parâmetros de substituição de linha do tempo de FW, quando ptcueformat=nbc é usado e o fluxo é um fluxo VOD com dicas no manifesto e anúncios integrados.

* Limpe o campo user-agent no cabeçalho HTTP antes de encaminhar para provedores de anúncios de terceiros/CDN.

* Filtre os caracteres de controle/não imprimíveis (código ascii &lt; 32) dos cabeçalhos HTTP &quot;agente-usuário&quot; antes de enviar para o Auditude e outros provedores de anúncios, CDNs. Auditude Ad-Call usado para falhar em cabeçalhos inválidos.

* Expurgue objetos V1 antigos de grupos NetStorage para manter a contagem de objetos dentro dos limites seguros do Akamai.

## Problemas resolvidos

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida. Por exemplo, ZD#xxxxx.

**PTAI 20.3.3**

* Problema com cabeçalhos X-Forwarded-For, nos quais os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentam incorretamente em certos cenários

## Problemas conhecidos e limitações

**PTAI 20.3.3**

Nenhuma nova limitação foi adicionada.
