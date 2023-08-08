---
title: Relatórios de uso de monitoramento de simultaneidade
description: Relatórios de uso de monitoramento de simultaneidade
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Relatórios de uso de monitoramento de simultaneidade {#cm-usage-reports}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.



## Visão geral {#usage-rep-overview}

A variável **Relatórios de uso de monitoramento de simultaneidade** O serviço está disponível por meio de uma API REST que fornece informações sobre o uso simultâneo, conforme relatado pelos aplicativos do cliente.

## Pré-requisitos {#usage-rep-prerequisites}

Para acessar o produto Relatórios de uso de monitoramento de simultaneidade, um cliente deve primeiro entrar em contato com o monitoramento de simultaneidade [Equipe de suporte](mailto:tve-support@adobe.com) e executarão as etapas necessárias para permitir acesso ao produto da API.

## Métricas e detalhamentos gerais de relatório {#general-rep-metrics-breakdown}

### Os usuários do Relatórios de uso podem monitorar as seguintes métricas:{#monitor-metrics}

| Nome | Descrição |
|:---|:---|
| ative-users | número de contas de usuários distintas que iniciaram pelo menos uma sessão de streaming durante o intervalo, detalhado pela granularidade de tempo |
| ative-sessions | número de sessões de transmissão que relataram atividade durante o intervalo (não inclui tentativas com falha, sessões que receberam uma resposta de negação para a chamada de inicialização) |
| started-sessions | número de sessões de streaming que foram iniciadas dentro do intervalo |
| completed-sessions | número de sessões de streaming que foram concluídas durante o intervalo (explicitamente ou devido ao tempo limite) |
| tentativas com falha | número de tentativas de inicialização de sessão que receberam uma resposta de negação |
| sessões descartadas | número de sessões de streaming que foram concluídas durante a reprodução (na pulsação) devido a uma violação de política. Essa métrica é significativa somente onde uma política FIFO ou last_one_wins é implementada. |
| dead-sessions | número de sessões de transmissão que foram explicitamente interrompidas ao iniciar uma nova sessão (por meio do cabeçalho X-Terminate) |
| duration_0-15 | número de fluxos com duração entre 0 e 15 minutos |
| duration_15-30 | número de fluxos com duração entre 15 e 30 minutos |
| duration_30-60 | número de fluxos com duração entre 30 e 60 minutos |
| duration_60-120 | número de fluxos com duração entre 60 e 120 minutos |
| duration_2h-4h | número de fluxos com duração entre 2 horas (120 minutos) e 4 horas |
| duração_4h-8h | número de fluxos com duração entre 4 horas e 8 horas |
| duration_8h-16h | número de fluxos com duração entre 8 horas e 16 horas |
| duration_16h-1d | número de fluxos com duração entre 16 horas e 1 dia (24 horas) |
| duration_1d-3d | número de fluxos com duração entre 1 dia e 3 dias |
| duration_3d-7d | número de fluxos com duração entre 3 dias e 7 dias |
| duration_1w-1m | número de fluxos com duração entre 1 semana (7 dias) e 1 mês (30 dias) |
| duration_over-1m | número de fluxos com duração superior a 1 mês (30 dias) |

### Os usuários dos Relatórios de uso podem filtrar as métricas listadas acima pelas seguintes dimensões: {#dimensions-2-filter-metrics}

| Nome do Dimension | Descrição |
|:---|:---|
| ano | O ano de 4 dígitos |
| mês | O mês do ano (1-12) |
| dia | O dia do mês (1-31) |
| hora | A hora do dia |
| minuto | O minuto da hora |
| aplicativo | O nome do aplicativo registrado no Monitoramento de Simultaneidade usado para gerenciar sessões |
| application-id | A ID do aplicativo registrada no Monitoramento de simultaneidade usada para gerenciar sessões |
| channel | Os metadados do canal enviados durante a inicialização da sessão (marcado como Desconhecido se nenhum metadado for enviado) |
| mvpd | O MVPD fornecido na gestão da sessão |
| platform | Os metadados da plataforma fornecidos na inicialização da sessão ou predefinidos para um aplicativo no nível de configuração |

## Detalhamentos e métricas do relatório de simultaneidade {#concurrency-reports-metrics-breakdown}

A partir da versão 2.9.0 do Monitoramento de simultaneidade, introduzimos um novo relatório para entender o uso simultâneo: um histograma do **nível de concorrência** e **nível de atividade**.

O objetivo principal deste relatório é ajudá-lo a entender o impacto de definir uma política com determinado limite de simultaneidade e fornecer informações suficientes para decidir se você deve aumentar o limite.

### Os usuários do Relatórios de uso podem monitorar as seguintes métricas: {#metrics-usage-rep-users}

| Nome do Dimension | Descrição |
|:---|:---|
| usuários | número de usuários que atingiram cada nível de concorrência/atividade |

### Os usuários dos Relatórios de uso podem filtrar as métricas listadas acima pelas seguintes dimensões: {#dimensions-to-filter-metrics}

| Nome do Dimension | Descrição |
|:---|:---|
| ano | O ano de 4 dígitos |
| mês | O mês do ano (1-12) |
| dia | O dia do mês (1-31) |
| nível de concorrência | Representa qualquer **atividade de fluxo aprovada na fase de inicialização da sessão** para que um usuário possa observar quantos fluxos simultâneos **foram abertos** por um usuário e compreender o impacto da aplicação de um determinado limite de simultaneidade |
| nível de atividade | Representa qualquer **atividade de fluxo (independentemente do estado: iniciada, ativa, interrompida, rejeitada)** para um usuário poder observar quantos fluxos simultâneos foram tentados de ser abertos por um usuário e entender o impacto da aplicação de um determinado limite de simultaneidade |
| mvpd | O MVPD fornecido na gestão da sessão |