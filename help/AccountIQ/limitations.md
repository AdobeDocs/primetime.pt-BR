---
title: Limitações e problemas conhecidos
description: Problemas conhecidos no produto.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Problemas conhecidos e limitações {#known-issues}

O Adobe se esforça para oferecer funcionalidades robustas e experiências ininterruptas para o usuário por meio de suas ofertas. A versão atual (versão 1.1) do Account IQ fornece análises de uso e compartilhamento de assinatura a provedores de streaming com alto grau de confiança. No entanto, as seguintes limitações serão abordadas nas versões futuras do .

* Ao definir coortes no painel ou nas páginas de relatórios, atualmente não há opção para adicionar métricas como **número de dispositivos** para refinar o segmento. Esse recurso estará disponível em breve.

* Ao estimar as pontuações de compartilhamento para contas individuais, o Account IQ adota uma abordagem conservadora que permite que as empresas atuem no compartilhamento com grande grau de confiança. No entanto, esta abordagem tende a subestimar a quantidade total de compartilhamento quando agregada em muitas contas.

* O [Pontuação de compartilhamento geral](/help/AccountIQ/dashboard.md#overall-sharing-score) atualmente, somente fatores em [Nível de compartilhamento](/help/AccountIQ/dashboard.md#sharing-level) e [Uso de contas compartilhadas](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). As versões futuras terão em conta métricas adicionais.

* Ao definir coortes no painel ou nas páginas de relatórios, os seletores de MVPDs e canais não têm o mecanismo de pesquisa, a partir de agora.

* Ao definir coortes no painel ou nas páginas de relatórios, há uma limitação para selecionar apenas até 10 MVPDs e Programadores (ou canais individuais).

* A opção de exportar estatísticas da conta está limitada à exportação de contas 1000, a partir de agora.

* A opção para selecionar [Tipo de segmento](#segment-type) quando a definição de Operações estiver limitada a **Número fixo de contas**. O **Número variável de contas** estará disponível em uma versão futura.

* As seções Avaliação de desempenho, Modelos de detecção, Segmentos, Snapshots e Regras na navegação à esquerda estão atualmente desativadas e estarão disponíveis em uma versão futura.

* Ao criar [operações](/help/AccountIQ/operation-affecting-user-segment.md), você pode identificar apenas dois tipos de [Ações](/help/AccountIQ/operation-affecting-user-segment.md) a partir de agora — Regras de monitoramento de simultaneidade e Ações externas.

* Atualmente, as Operações só podem ser criadas e [agendado](/help/AccountIQ/operation-affecting-user-segment.md#action). As versões futuras permitirão pausá-las, retomá-las e gerenciá-las totalmente.

* Devido ao conjunto mais limitado de dados usados, o modo de isolamento não reflete verdadeiramente a quantidade de compartilhamento. Portanto, o MVPD no modo de isolamento não pode ser comparado a qualquer outro MVPD. <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* Ao definir um novo [segmento](/help/AccountIQ/segments-timeframe.md) para uma operação, você pode adicionar métricas. Mas, se você selecionar um segmento salvo, não será possível adicionar mais métricas para refinar o segmento.

* A granularidade e o seletor de período são limitados a uma semana ou um mês, o que significa que os dados podem ser avaliados em uma única semana ou em um único mês.

* Intervalos predefinidos estão atualmente desativados em granularidade e seletor de período de tempo e estarão disponíveis em uma versão futura.
