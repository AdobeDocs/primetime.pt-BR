---
title: Operações no QI da conta
description: As operações no Account IQ envolvem a execução de ações para realizar automações e operações em massa em contas de assinantes e acompanhar seus efeitos.
source-git-commit: e61cca77bad4f01de871e300dc99d7368c283f2a
workflow-type: tm+mt
source-wordcount: '506'
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

   O relatório é exibido no formato de um gráfico de barras empilhadas.

   ![](assets/operation-impact-report.png)

   *Figura: Relatório de operações para visualizar os impactos das operações*

   O eixo x representa o período de avaliação e o eixo y representa uma variável para medir o impacto da operação.

   Por exemplo, na imagem acima, a variável no eixo y é o número de contas. Ao examinar o gráfico, você pode comparar o número de contas que estão no segmento de operações com o número de contas que estão fora do segmento de operações em um determinado momento (como a segunda semana do período de avaliação de operações). Portanto, você pode analisar como, durante o período de avaliação, o número de contas varia dentro e fora do segmento da operação.

   Portanto, se sua operação era enviar emails de aviso para contas suspeitas, e as contas em operações eram aquelas com probabilidade de compartilhamento superior a 90 e usando mais de 5 dispositivos para transmitir conteúdo, então no início do período de avaliação as contas no segmento são mais de 7 milhões. Este número é alterado durante o período de avaliação, tal como indicado no gráfico, indicando assim o impacto do funcionamento. Com base na avaliação, você pode tomar medidas corretivas em relação a contas suspeitas, ou continuar a operação, ou ajustar sua estratégia para melhores resultados para reduzir o compartilhamento de credenciais.

2. Para fechar o relatório e voltar à página principal de Operações, selecione **Operações** opção em **Ações** na navegação à esquerda.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->