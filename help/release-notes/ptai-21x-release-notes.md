---
title: Notas de versão do PTAI 21.8.1
description: As notas de versão da PTAI descrevem as novidades ou alterações, os problemas resolvidos e conhecidos no Primetime Ad Insertion no ano de 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: 97a192ed1d0ddc034f72a836a70293acfcca9881
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Notas de versão do Primetime Ad Insertion 21.8.1

As notas de versão do Primetime Ad Insertion 21.x.x descrevem as novidades ou alterações, os problemas resolvidos e os problemas conhecidos no Primetime Ad Insertion em 2021

<!---
Primetime Ad Insertion 21.9.1
When: Tuesday, September 7, 2021 from 02:30 AM to 05:30 AM EASTERN









What:  Primetime Ad Insertion 21.9.1

When:  Tuesday, September 7, 2021 from 02:30 AM to 05:30 AM Eastern Time

Changes:

* Updates to infrastructure components behind PTAI’s mediation and reporting components (Primetime Ads GUI)
-->

## Novidades do PTAI 21.8.1

Quando: Terça-feira, 24 de agosto de 2021, das 2:00 AM às 05:00 Hora do leste

* Adição de suporte para fluxos DASH Live/ Linear (VOD já tem suporte).

## Aprimoramentos e correções nas versões anteriores

### Versão 21.5.1

Quando:  Quarta-feira, 26 de maio de 2021, das 3:30 às 06:30 Hora do Leste

**Alterações**

* Adição de suporte para o tipo de segmentação obsoleta 0x01 (UPID) para formatos de sinalização baseados em SCTE.

* Nova telemetria adicionada para alterações futuras do painel.

### Versão 21.4.1

**Quando:** quinta-feira, 22 de abril de 2021, das 2:00 AM às 5:00 Hora do leste

**Alterações**

* A limitação de solicitação de sessão será ativada para proteção contra possíveis ataques de DDOS. As sessões serão limitadas a 10 solicitações por segundo, com um limite de 100 solicitações em fila. Não prevemos qualquer impacto nos jogadores que se comportam de acordo com as especificações de HLS/DASH.

* Outras melhorias de manutenção e segurança

### Versão 21.2.2

**Quando:** terça-feira, 23 de fevereiro de 2021, das 1:00 AM às 04:00 Hora do leste

**Alterações**

* Adição de suporte para inserção/sincronização de fluxo EXT-X-IMAGE-STREAM-INF em fluxos HLS. O recurso é ativado por meio de uma configuração do lado do servidor. Entre em contato com seu representante de conta técnica para ativar o recurso.

### Versão 21.2.1

**Quando:** quarta-feira, 3 de fevereiro de 2021, das 1:00 AM às 04:00 Hora do leste

**Alterações**

* Adição de suporte para otimização de saída DASH: consolidação de nós baseada em tempo.

### Versão 21.1.2

**Quando:** terça-feira, 19 de janeiro de 2021, das 12:30 às 08:30 Hora do leste

**Alterações**

* Atualização de manutenção: Atualização de clusters de cache de memória back-end do Primetime Ad Insertion.

### Versão 21.1.1

**Quando:** quarta-feira, 13 de janeiro de 2021, das 01:00 às 04:00 Hora do leste

**Alterações**

* Adição de suporte para disponibilidade de afiliadas para formatos de sinalização baseados em SCTE35.
