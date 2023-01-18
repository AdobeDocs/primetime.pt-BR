---
title: Definir um segmento e um período
description: Definir um segmento e um período
exl-id: 86fe010d-3202-4ce2-b803-ff44f5538d7e
source-git-commit: c17fb003d8c8103aac36696f696c9e3c7bb83c4f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Definir um segmento e um período {#define-segment}

Todas as análises ou exibições de relatórios no QI da conta começam com a definição do segmento e a seleção do período de avaliação. [Segmento](/help/AccountIQ/product-concepts.md#segmet-def) refere-se a todos os assinantes ou visualizadores que atendem aos seus critérios (assinatura de um MVPD e exibição de canais específicos) de avaliação.

![](assets/segment-panel.png)

*Figura: Seleção de segmento e período*

Na parte superior de todas as páginas de relatórios do Account IQ, há um painel para definir segmentos selecionando MVPDs, programadores de canais e granularidade e período.

## Seleção de segmento {#select-segment}

### Selecionar MVPDs no segmento {#select-segment-mvpds}

Para selecionar MVPDs de **MVPDs no segmento** opção:

1. Clique ou toque no **MVPDs no segmento** opção suspensa.

   >[!NOTE]
   >
   >**Todos** MVPDs do setor são selecionados por padrão. Aqui, você pode selecionar uma das opções **Os 10 MVPDs principais por pontuação de compartilhamento**, **Os 10 MVPDs principais por utilização**, **Os 10 MVPDs principais por conta** ou MVPDs individuais. No entanto, para selecionar MVPDs individuais, você precisa desmarcar **Todos**.

1. Clique ou toque nos MVPDs desejados.

   Você pode remover um MVPD da seleção ao desmarcá-lo.

1. Clique ou toque em **Aplicar seleção** para que sua seleção entre em vigor. Caso contrário, você perderá a seleção feita.

   >[!NOTE]
   >
   >Se você selecionar o Modo de isolamento, nenhum dos outros MVPDs poderá ser selecionado.

### Selecionar canais no segmento {#select-segment-channels}

Para selecionar os canais do programador desejado na **Canais no segmento** opção:

1. Clique ou toque no **Canais no segmento** opção suspensa.

   >[!NOTE]
   >
   >**Todos** os canais do programador para sua empresa são selecionados por padrão. Para selecionar canais ou programadores individuais, primeiro desmarque **Todos**.

1. Clique ou toque nos canais ou programadores desejados.

   Os itens da lista de nível superior na **Canais no segmento** são [programador](/help/AccountIQ/product-concepts.md#programmer-def) as empresas e os itens de lista sob nomes de programadores são seus [canais](/help/AccountIQ/product-concepts.md#channel-def). Você pode selecionar canais individuais em programadores ou selecionar programadores e todas as atividades dos canais sob esse programador são incluídas nos resultados do relatório e do gráfico.

   ![](assets/programmer-channels.png)


   *Figura: Programadores e canais listados no seletor de canais*

   >[!IMPORTANT]
   >
   >Os resultados da seleção de canais individuais em um programador não são os mesmos que os da seleção do programador.
   >
   >
   >Quando você seleciona canais individuais, as atividades desses canais são detalhadas individualmente em alguns relatórios. No entanto, ao selecionar o programador principal de todos esses canais, todas as atividades desses canais serão incluídas, mas não serão analisadas individualmente nos relatórios.

1. Clique ou toque em **Aplicar seleção** para que sua seleção entre em vigor.

>[!NOTE]
>
>Não é possível selecionar mais de 10 itens nos menus suspensos do MVPD ou do programador.

### Desmarcar MVPDs e canais {#deselect-segment-mvpds-channels}

Além de alterar sua seleção no **MVPDs no segmento** e **Canais no segmento** seletores de segmentos, você pode desmarcar os MVPDs e canais selecionados anteriormente ao:

* Selecionar o **Remover** ícone (![ícone remover](assets/remove-icon.png)) nos nomes desses MVPDs e canais selecionados, exibidos abaixo do seletor de segmentos.

* Você também pode usar **Limpar seleção** para remover todos os MVPDs ou canais selecionados anteriormente.

![](assets/segment-panel-selection.png)

*Figura: MVPDs e canais selecionados no painel de segmento e período*

## Granularidade e seleção de período {#granularity-timeframe}

Para selecionar um período de avaliação:

1. Selecione o **Granularidade e período** seletor de data.

1. Selecione um **Semana** ou **Mês** from **Agregar por** para definir a granularidade para sua avaliação.

   ![](assets/granularity-timeframe-weekwise.png)


   *Figura: Seletor de data para selecionar Granularidade e período*

1. Após selecionar a granularidade, você pode usar setas para frente ou para trás para avançar ou para trás no tempo.

1. Especifique um período no passado (em mês ou semana com base na granularidade selecionada) para avaliação.

1. Selecionar **Aplicar seleção** para garantir que sua seleção entre em vigor.
