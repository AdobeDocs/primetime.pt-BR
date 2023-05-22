---
title: Notas de versão do PTAI 21.11.1
description: As notas de versão do PTAI descrevem o que é novo ou alterado, os problemas resolvidos e conhecidos no Primetime Ad Insertion no ano de 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: f4c6ef44c7f13bf8170a1f23a7ae8eba0171316a
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Notas de versão do Primetime Ad Insertion 21.11.1

As notas de versão do Primetime Ad Insertion 21.xx.x descrevem o que é novo ou alterado, problemas resolvidos e problemas conhecidos no Primetime Ad Insertion no ano de 2021.

## Novidades na PTAI 21.11.1

Quando: Terça-feira, 9 de novembro de 2021 das 1:30 às 04:30 Horário do Leste

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] agora pode ser configurado por região.

* O Roku Trick Play é totalmente compatível.

## Aprimoramentos e correções em versões anteriores

### Versão 21.10.1

Quando: Terça-feira, 12 de outubro de 2021 das 7:45 às 13:45 Horário do Leste

* Servidores consolidados, servidores removidos de não produção e não úteis.

### Versão de manutenção do Primetime Ad Insertion

Quando: Terça-feira, 28 de setembro de 2021 das 5h às 6h Horário do Leste

* Atualizações na pilha de Balanceador de carga do Balanceador de carga elástico do AWS para o Balanceador de carga de aplicativo do AWS para obter funcionalidade e escalabilidade aprimoradas. Esses Balanceadores de carga são usados para rotear o tráfego de solicitação de anúncio para o back-end do Auditude a partir da camada de Ad Insertion (SSAI/CSAI).

### Versão 21.9.1

Quando: Terça-feira, 7 de setembro de 2021 das 02:30 às 05:30, horário do leste dos EUA

* Atualizações dos componentes de infraestrutura por trás dos componentes de mediação e relatórios do Primetime Ad Insertion (GUI de anúncios do Primetime).

### Versão 21.8.1

Quando: Terça-feira, 24 de agosto de 2021 das 2h às 5h Horário do Leste

* Adição de suporte para DASH Live/ fluxos lineares (VOD já é suportado).

### Versão 21.5.1

Quando: Quarta-feira, 26 de maio de 2021 das 3:30 às 06:30, horário do leste dos EUA

**Alterações**

* Adição de suporte para o tipo de segmentação obsoleta 0x01 (UPID) para formatos de sinalização baseados em SCTE.

* Adição de nova telemetria para alterações futuras do painel.

### Versão 21.4.1

**Quando:** Quinta-feira, 22 de abril de 2021 das 2:00 às 5:00 Horário do Leste

**Alterações**

* A limitação de solicitações de sessão será ativada para proteger contra possíveis ataques de DDOS. As sessões serão limitadas a 10 solicitações por segundo, com um limite máximo de 100 solicitações em fila. Não prevemos qualquer impacto sobre os jogadores que se comportam de acordo com as especificações HLS/DASH.

* Outras melhorias de manutenção e segurança

### Versão 21.2.2

**Quando:** Terça-feira, 23 de fevereiro de 2021 de 1:00 às 04:00 Horário do Leste

**Alterações**

* Adição de suporte para inserção/sincronização de fluxo EXT-X-IMAGE-STREAM-INF em fluxos HLS. O recurso é ativado por meio de uma configuração do lado do servidor. Entre em contato com seu representante técnico de conta para ativar o recurso.

### Versão 21.2.1

**Quando:** Quarta-feira, 3 de fevereiro de 2021, das 1:00 às 04:00, horário do leste dos EUA

**Alterações**

* Adição de suporte para otimização de saída DASH: consolidação de nó baseada em tempo.

### Versão 21.1.2

**Quando:** Terça-feira, 19 de janeiro de 2021 das 12:30 às 08:30 Horário do Leste

**Alterações**

* Atualização de manutenção: atualização de clusters de memcache de back-end de Ad Insertion do Primetime.

### Versão 21.1.1

**Quando:** Quarta-feira, 13 de janeiro de 2021, das 01:00 às 04:00, horário do leste dos EUA

**Alterações**

* Adição de suporte para disponibilidades afiliadas para formatos cue baseados em SCTE35.
