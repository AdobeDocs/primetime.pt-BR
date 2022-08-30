---
title: Operações no QI da conta
description: As operações no Account IQ envolvem a execução de ações para realizar automações e operações em massa em contas de assinantes e acompanhar seus efeitos.
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 5b34fbe26078ae761d61179975366505c5628c9c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Operações {#operations-tab-next-steps}

Depois de entender os padrões de uso dos assinantes e identificar o compartilhamento de senha para o segmento selecionado (usando relatórios e análises no Account IQ), você pode realizar ações direcionadas para um objetivo de reduzir o compartilhamento de senha.

A funcionalidade Operações no Account IQ ajuda você a lidar e gerenciar efetivamente o compartilhamento de credenciais por meio de procedimentos focalizados chamados de operações. Ele oferece opções para projetar ações objetivas e direcionadas (com base no objetivo) para um grupo específico de contas de assinantes e automatizar a execução por uma duração futura. Por meio da funcionalidade Operações , você pode não apenas criar e executar operações, mas também medir seus impactos. Portanto, ao medir os impactos, você pode ajustar sua estratégia para otimizar o efeito, seja convertendo mutuários ou reduzindo o compartilhamento de credenciais.

Para exibir **Operações** seleção de página **Operações** opção em **Ações** na navegação à esquerda do aplicativo Account IQ. A página Operações lista todas as operações já existentes no sistema de QI da conta, juntamente com seus detalhes.

![](assets/operations-page.png)

*Figura: Lista e detalhes das operações existentes no Account IQ*

Na página Operações, é possível:

* Exibir uma lista de operações já existentes no Account IQ

* Exibir detalhes da operação, como:

   * status (Programado, Em Execução, Encerrado, Erro ou Interrompido)

   * andamento (em porcentagem de conclusão)

   * público-alvo (segmento para executar a operação)

   * horário (data de início e de término da operação)

   * criação e data final da operação

* [Criar nova operação](/help/AccountIQ/operation-affecting-user-segment.md)

* [Exibir relatórios de operação](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## Exibir relatórios de operação {#operation-reports}

Você pode analisar os impactos de uma operação ao visualizar seu relatório. Para exibir o relatório de uma operação:

1. Selecione o nome da operação na página principal de Operações.

   O relatório é exibido no formato de um gráfico de coluna empilhada.

   ![](assets/operation-impact-report.png)

   *Figura: Relatório de operações para visualizar os impactos das operações*

   O eixo X representa o período de avaliação e o eixo y descreve o impacto da operação (em termos de número de contas num segmento durante o período de avaliação). Cada barra é dividida em três partes.

   * Uma parte representa o número de contas que ainda atendem aos critérios do segmento de operação.

   * Outra parte representa o número de contas ativas para o período que estavam originalmente no segmento, mas não atendem mais aos critérios do segmento de operação.

   * A terceira parte representa as contas que não estavam ativas nesse período.
   >[!NOTE]
   >
   >A Primeira barra representa o número de contas que atendem às condições do segmento de operação no início do período de avaliação.

   Com o tempo, o gráfico mostra o efeito de sua ação (por meio da operação), indicando o número de contas que alteraram seu comportamento em relação aos critérios originais (por exemplo, ter probabilidade de compartilhamento superior a 90 e usar mais de 5 dispositivos) ou ficaram inativas.

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. Para fechar o relatório e voltar à página principal de Operações, selecione **Operações** opção em **Ações** na navegação à esquerda.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->