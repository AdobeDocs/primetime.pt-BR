---
title: Notas de versão do PTAI 20.5.1
description: As notas de versão PTAI 20.5.1 descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos na inserção do anúncio dinâmico Primetime no ano 2020.
translation-type: tm+mt
source-git-commit: e5fb84a7199e16a5eb7b6fd61aa7a1e50bb05c73
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# Notas de versão do Primetime Dynamic Ad Insertion 20.5.1

As notas de versão do Dynamic Ad Insertion 20.5.1 descrevem o que é novo ou alterado, os problemas resolvidos e os problemas conhecidos no Primetime Dynamic Ad Insertion no ano 2020.

## Novidades do PTAI 20.5.1

**Quando:** terça-feira, 5 de maio de 2020 das 04:00 às 05:00 Hora do Leste

* Correção de um problema para garantir que cabeçalhos CORS corretos sejam fornecidos quando cabeçalhos If-Modifiados-Since são enviados.

* Correções de erros no painel CRS.

* Atualizações de manutenção.

## O que mudou em versões anteriores

### Versão 20.3.4

**Quando:** quarta-feira, 1 de abril de 2020, das 03:00 às 04:00, horário do leste

* Corrigido um problema que fazia com que as legendas ficassem fora de sincronização após a inserção do anúncio no VOD/ WebVTT.

* Atualizações de segurança.

### Versão 20.3.3

**Quando:** quinta-feira, 26 de março de 2020, das 03h00 às 04h00, horário do leste

* As respostas SSAI 4XX e 5XX agora fornecem corretamente cabeçalhos relacionados ao CORS, permitindo que clientes de exibição da Web javascript entre domínios leiam com êxito respostas de erro.

* Correção de um problema com cabeçalhos X-Forwarded-For, em que os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Correção de um problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentavam incorretamente.

### Versão 20.3.2

**Quando:** quarta-feira, 11 de março de 2020, das 05:30 às 07:00 Hora do Leste

* Melhorias no tratamento do sinal SCTE35.

* Atualizações de manutenção.

### Versão 20.3.1

**Quando:** quinta-feira, 5 de março de 2020, das 02h30 às 04h30, horário do leste

* Melhorias no desempenho:

   * Adição do suporte de cache para manifestos m3u8 mestres/de mídia. Esses manifestos agora respondem ao Cache-Control: cabeçalhos public e Max-Age, que geralmente podem melhorar o desempenho do start de vídeo.

   * Adição de suporte para forçar a busca de criações https em http, o que também pode melhorar o desempenho do start de vídeo.

* Correções de segurança e manutenção.

### Versão 20.2.1

**Quando:** quinta-feira, 13 de fevereiro de 2020, das 04:30 às 05:30, horário do leste

* Adicionado suporte para a sutura de ativos de anúncios que contêm vários fluxos somente de áudio com base no idioma/codec/taxa de bits.
* Pequenas melhorias de desempenho e atualizações de manutenção.

### Versão 20.1.3

**Quando:** terça-feira, 28 de janeiro de 2020, das 2h00 às 03h00, horário do leste

* **VMAP com suporte FER para nbc CueFormat**

   Converta dicas do fluxo FER em parâmetros de substituição de linha do tempo FW quando `ptcueformat=nbc` são usadas e o fluxo é um fluxo VOD com dicas no manifesto e anúncios integrados.

* Limpe o campo user-agent no cabeçalho HTTP antes de encaminhar para provedores de anúncios de terceiros/ CDN.

* Filtre os caracteres de controle/não imprimíveis (código ASCII &lt; 32) dos cabeçalhos HTTP agente-usuário antes de enviar para o Auditude e outros provedores de anúncios, CDNs. Auditude Ad-Call usado para falhar em cabeçalhos inválidos.

* Expurgue objetos V1 antigos de grupos NetStorage para manter a contagem de objetos dentro dos limites seguros do Akamai.

### Versão 20.1.2 (Hotfix)

**Quando:** segunda-feira, 20 de janeiro de 2020, das 02h00 às 03h00, horário do leste

* Atualizações de manutenção.

### Versão 20.1.1

**Quando:** quarta-feira, 15 de janeiro de 2020, das 04:00 às 05:00, horário do leste

* O Creative Repacking Service agora oferece uma inserção de anúncios mais rápida ao adicionar automaticamente anúncios de criação malformados.

* Adicionado suporte de fase 1 para o novo formato de sinalização SCTE 35 na inserção de anúncios no servidor.

* Atualizações de manutenção.

## Problemas resolvidos

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida. Por exemplo, `ZD#xxxxx`

**PTAI 20.5.1**

* Problemas com cabeçalhos CORS quando os cabeçalhos If-Modifique-Since são enviados.

* Problemas no painel CRS.

**PTAI 20.3.4**

* Problema que fazia com que as legendas ficassem fora de sincronização após a inserção do anúncio no VOD/ WebVTT.

**PTAI 20.3.3**

* Problema com cabeçalhos X-Forwarded-For, nos quais os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentam incorretamente em certos cenários

## Problemas conhecidos e limitações

**PTAI 20.3.3**

Nenhuma nova limitação foi adicionada.
