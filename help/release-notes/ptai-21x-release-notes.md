---
title: Notas de versão do PTAI 21.11.1
description: As notas de versão da PTAI descrevem as novidades ou alterações, os problemas resolvidos e conhecidos no Primetime Ad Insertion no ano de 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: b58fea35be528c4c030eab39fde9dd642d90cb58
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Notas de versão do Primetime Ad Insertion 21.11.1

As notas de versão do Primetime Ad Insertion 21.xx.x descrevem as novidades ou alterações, os problemas resolvidos e os problemas conhecidos no Primetime Ad Insertion em 2021.

## Novidades do PTAI 21.11.1

Quando: terça-feira, 9 de novembro de 2021, das 1:30 às 04:30 Hora do leste

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] agora é configurável por zona.

## Aprimoramentos e correções nas versões anteriores

### Versão 21.10.1

Quando: Terça-feira, 12 de outubro de 2021, das 7h45 às 13h45, Hora do Leste

* Servidores consolidados, servidores não relacionados à produção e não úteis removidos.

### Versão de manutenção do Primetime Ad Insertion

Quando: Terça-feira, 28 de setembro de 2021, das 5:00 AM às 6:00 Hora do Leste

* Atualizações da pilha de Balanceador de Carga da AWS que  Balanceador de Carga Elástico para o Balanceador de Carga da Aplicação AWS para obter funcionalidades e escalabilidade aprimoradas. Esses balanceadores de carga são usados para rotear e solicitar tráfego para o backend do Auditude da camada de Ad Insertion (SSAI/CSAI).

### Versão 21.9.1

Quando: terça-feira, 7 de setembro de 2021, das 02:30 às 05:30 Hora do leste

* Atualizações dos componentes de infraestrutura por trás dos componentes de mediação e de relatórios do Primetime Ad Insertion (GUI do Primetime Ads).

### Versão 21.8.1

Quando: Terça-feira, 24 de agosto de 2021, das 2:00 AM às 05:00 Hora do leste

* Adição de suporte para fluxos DASH Live/ Linear (VOD já tem suporte).

### Versão 21.5.1

Quando: Quarta-feira, 26 de maio de 2021, das 3:30 às 06:30 Hora do Leste

**Alterações**

* Adição de suporte para o tipo de segmentação obsoleta 0x01 (UPID) para formatos de sinalização baseados em SCTE.

* Nova telemetria adicionada para alterações futuras do painel.

### Versão 21.4.1

**Quando:** Quinta-feira, 22 de abril de 2021, das 2:00 AM às 5:00 Hora do Leste

**Alterações**

* A limitação de solicitação de sessão será ativada para proteção contra possíveis ataques de DDOS. As sessões serão limitadas a 10 solicitações por segundo, com um limite de 100 solicitações em fila. Não prevemos qualquer impacto nos jogadores que se comportam de acordo com as especificações de HLS/DASH.

* Outras melhorias de manutenção e segurança

### Versão 21.2.2

**Quando:** Terça-feira, 23 de fevereiro de 2021, das 1:00 AM às 04:00 Hora do leste

**Alterações**

* Adição de suporte para inserção/sincronização de fluxo EXT-X-IMAGE-STREAM-INF em fluxos HLS. O recurso é ativado por meio de uma configuração do lado do servidor. Entre em contato com seu representante de conta técnica para ativar o recurso.

### Versão 21.2.1

**Quando:** Quarta-feira, 3 de fevereiro de 2021, das 1:00 AM às 04:00 Hora do leste

**Alterações**

* Adição de suporte para otimização de saída DASH: consolidação de nós baseada em tempo.

### Versão 21.1.2

**Quando:** terça-feira, 19 de janeiro de 2021, das 12:30 às 08:30 Hora do leste

**Alterações**

* Atualização de manutenção: Atualização de clusters de cache de memória back-end do Primetime Ad Insertion.

### Versão 21.1.1

**Quando:** Quarta-feira, 13 de janeiro de 2021, das 01:00 AM às 04:00 Hora do leste

**Alterações**

* Adição de suporte para disponibilidade de afiliadas para formatos de sinalização baseados em SCTE35.
