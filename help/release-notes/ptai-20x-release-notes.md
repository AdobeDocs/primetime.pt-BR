---
title: Notas de versão do PTAI 20.3.3
description: As notas de versão PTAI 20.3.3 descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos na inserção do anúncio dinâmico Primetime no ano 2020.
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Notas de versão do Primetime Dynamic Ad Insertion 20.3.3

As notas de versão do Dynamic Ad Insertion 20.3.3 descrevem o que é novo ou alterado, os problemas resolvidos e os problemas conhecidos no Primetime Dynamic Ad Insertion no ano 2020.

## Novidades do PTAI 20.3.3

**Quando:** quinta-feira, 26 de março de 2020, das 03h00 às 04h00 do ORIENTE

* As respostas SSAI 4XX e 5XX agora fornecem corretamente cabeçalhos relacionados ao CORS, permitindo que clientes javascript/webview entre domínios leiam com êxito respostas de erro.

* Correção de um problema com cabeçalhos X-Forwarded-For, em que os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Correção de um problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE incrementavam incorretamente

## O que mudou em versões anteriores

### Versão

**Quando:**

### Versão

**Quando:**

## Problemas resolvidos

Quando a resolução estiver associada a um problema reportado, uma referência do Zendesk será exibida. Por exemplo, ZD#xxxxx.

**PTAI 20.3.3**

* Problema com cabeçalhos X-Forwarded-For, nos quais os endereços IPv6 não eram corretamente codificados por URL quando passados para os servidores de publicidade.

* Problema com fluxos de áudio CMAF/descompilados, em que, em certos cenários, os números EXT-X-MEDIA-SEQUENCE aumentam incorretamente em certos cenários

## Problemas conhecidos e limitações

**PTAI 20.3.3**

Nenhuma nova limitação foi adicionada.
