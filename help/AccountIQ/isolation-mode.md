---
title: Exibir relatórios no modo de isolamento
description: Exiba relatórios no modo de isolamento do Xfinity.
exl-id: e7cf24c5-9bfa-48f6-b5c8-20443a976891
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Exibir relatórios compartilhados no modo de isolamento {#report-isolation-mode}

No modo de isolamento, os MVPDs (como Xfinity) identificam de forma consistente os assinantes em todos os dispositivos, mas identificam seus assinantes de forma diferente, com base nos programadores com os quais interagem. Enquanto que no modo padrão, os MVPDs identificam de forma consistente os assinantes entre dispositivos, independentemente dos programadores.

Por exemplo, na imagem a seguir, se um Assinante B de um MVPD de modo de isolamento (como Xfinity) acessar o conteúdo oferecido por dois programadores diferentes usando o mesmo dispositivo, o MVPD associará identificadores diferentes a duas tentativas de acesso diferentes. Assim, para esses programadores (L e M na figura) e para o Account IQ, parece que há dois assinantes diferentes acessando o conteúdo. No entanto, para o MVPD padrão, se o Assinante B acessar o conteúdo oferecido por dois programadores diferentes, o MVPD associará um único identificador de acesso para ambas as tentativas de acesso. Os MVPDs (como Xfinity) no Modo de isolamento não identificam consistentemente um assinante, mesmo que o assinante esteja usando o mesmo dispositivo em diferentes programadores.

![](assets/isolation-diff-new.png)

*Figura: Modo de isolamento MVPD identifica quatro assinantes diferentes em vez de dois*

Para gerenciar a distorção dos dados (devido à identificação do mesmo assinante que é diferente com base no acesso a diferentes programadores), o Modo de isolamento limita a atividade relatada sobre um programador à atividade somente nos aplicativos desse programador. Por exemplo, para o Modo de isolamento na imagem acima, o Programador L vê os dados com base apenas na atividade das Identidades W e Y, ignorando as Identidades X e Z.

>[!IMPORTANT]
>
> A desvantagem é que o Programador L é privado de compartilhar informações coletadas sobre os Assinantes A e B devido à atividade com qualquer Programador diferente de L.

No Modo de isolamento, todos os cálculos feitos para obter as Pontuações de compartilhamento e todas as métricas associadas são feitos usando apenas a atividade dos dispositivos que fazem streaming dos aplicativos que pertencem ao Programador e aos canais selecionados.
As pontuações de compartilhamento e probabilidades são calculadas somente usando o fluxo que começa a partir dos canais selecionados no momento.

Para exibir métricas no modo de isolamento:

1. Selecionar **modo de isolamento** do **MVPDs no segmento** opção suspensa e selecione **Aplicar seleção**.

   ![](assets/xfinity-in-segment.gif)

   *Figura: Seleção de MVPD no modo de isolamento*

1. Selecione os canais desejados no **Canais no segmento** opção suspensa e selecione **Aplicar seleção**. Além disso, selecione uma [período](/help/AccountIQ/product-concepts.md#granularity-def).

   >[!IMPORTANT]
   >
   >Como o compartilhamento de conta é mais relevante quando medido para transmissão em todos os aplicativos de Programadores, você verá menor Pontuação de compartilhamento e alguma variação nas métricas no Modo de isolamento.

   ![](assets/aggregate-sharing-isolation.png)

   *Figura: Compartilhamento de medidores de probabilidade no modo de isolamento*

   Observe que os gabaritos acima mencionados mostram que apenas 6% de todas as contas estão sendo compartilhadas; e apenas 8% do conteúdo está sendo consumido por esses 8%. Assim, os canais podem comparar suas pontuações no Modo de isolamento com aquelas entre os outros MVPDs. Por conseguinte, as informações obtidas através do modo de isolamento devem ser interpretadas de forma diferente dos outros dados.
