---
title: Exportar informações para contas com alta pontuação de compartilhamento
description: Exportar informações para contas com alta pontuação de compartilhamento.
exl-id: df41ddd2-fde3-4861-abd4-6e32f0be9ea5
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---

# Exportar informações para contas com alta pontuação de compartilhamento {#export-account-info-high-score}

O Account IQ oferece a opção de exportar detalhes de compartilhamento de conta para 1000 contas de assinantes principais com base em suas [compartilhando probabilidades](/help/AccountIQ/product-concepts.md#account-sharing-probability-def). Os dados no arquivo CSV exportado são classificados na ordem decrescente das probabilidades de compartilhamento das contas do assinante, dos MVPDs selecionados no [segmento](/help/AccountIQ/product-concepts.md#segment-def), por um [intervalo de tempo especificado](/help/AccountIQ/product-concepts.md#time-frame-def).

A opção para exportar as informações de compartilhamento de conta está disponível em [Relatórios de uso geral](/help/AccountIQ/general-usage-reports.md) e [Relatórios de Contas Compartilhadas](/help/AccountIQ/shared-acc-reports.md) páginas.

>[!NOTE]
>
>Os números no arquivo CSV baixado são diferentes para as páginas de relatórios Uso geral e Contas compartilhadas. Isso ocorre porque a página Relatórios de uso geral tem filtros adicionais para os programadores selecionarem Limite para o número de dispositivos, IPs e códigos postais. Portanto, os dados exportados dos relatórios de Uso geral são baseados no filtro de limite adicional aplicado.

![Opção Exportar em Uso geral](assets/export.png)

Para exportar as informações de compartilhamento de conta dos assinantes:

1. Defina um segmento desejado seguindo as etapas em [Como definir um segmento e selecionar o período](/help/AccountIQ/howto-select-segment-timeframe.md) para avaliação de [segmento e período](/help/AccountIQ/segments-timeframe.md) painel.

1. Selecione o **Exportar as 1000 contas principais** opção para exportar as informações da conta de 1000 assinantes com maior probabilidade de compartilhamento.

Quando você usa a opção de exportação, as estatísticas de 1000 contas com as maiores probabilidades de compartilhamento (para um intervalo de tempo definido) são baixadas para a pasta Downloads da sua máquina local.

>[!NOTE]
>
>O arquivo CSV baixado pode ser aberto usando qualquer aplicativo que leia o arquivo CSV, por exemplo, o Microsoft Excel.

![dados exportados em formato csv](assets/exported-csv.png)

*Figura: dados da conta compartilhada exportados no formato CSV*

## Colunas no relatório exportado {#columns-in-export}

**Semana/Mês**

A semana ou o mês selecionado no **Granularidade e intervalo de tempo** no seletor de segmentos, para o qual as estatísticas de compartilhamento são buscadas.

**MVPD**

Se você for um usuário programador, a coluna mostrará a qual MVPD a conta do assinante pertence.

**ID do Assinante**

Conta específica da qual estamos falando em uma linha.

**Nº Mínimo de Dispositivos**

O número real de dispositivos (esse conteúdo de fluxo) é quase certamente maior que o número mínimo de dispositivos, especificado para uma conta específica.

>[!NOTE]
>
>O número real de dispositivos (esse conteúdo de fluxo) é certamente maior que o número mínimo de dispositivos, especificado para uma conta específica.

**Nº Mínimo de Pessoas**

O número mínimo absoluto de pessoas que eram conteúdo de transmissão ativo usando esses dispositivos.

>[!NOTE]
>
>O número real de pessoas (esse conteúdo de fluxo) é quase certamente muito maior do que o número mínimo de pessoas, especificado para uma determinada conta.

**Nº de IPs**

Número de endereços IP dos quais o conteúdo é transmitido.

**Nº de Locais**

Número de locais (com base no código postal) dos quais o conteúdo é transmitido.

**Nº de Cidades**

Número de cidades onde ocorreu a transmissão.

**# Estados**

Número de estados em que o streaming ocorreu.

**Nº de Clusters**

O número de [clusters](/help/AccountIQ/product-concepts.md#cluster-def) onde ocorreu a transmissão.

**Extensão geográfica (milhas)**

A distância máxima entre os locais de streaming associados à conta.

**# AuthN OK**

O número de vezes que os usuários fizeram logon durante o período, usando essa conta.

**# AuthZ OK**

Número de vezes que um MVPD autorizou um fluxo ou concedeu acesso (ao conteúdo) a essa conta.

>[!NOTE]
>
>A variável **# AuthZ OK** está relacionado ao **Nº de Solicitações Play**; for menor que **Nº de Solicitações Play** porque o Adobe armazena em cache as autorizações que vêm para MVPDs normalmente por 24 horas.

**Nº de Solicitações Play**

O número real de fluxos durante o período.

**# Canais**

Número total de canais diferentes que a conta assistiu durante o período.

>[!NOTE]
>
>**# Canais** inclui os canais que não pertenciam necessariamente ao programador conectado.
>
>Esse número da conta foi exibido porque a conta assistiu ao seu canal, mas também acessou outros canais durante esse período.

**Padrão de uso**

Os números nesta coluna são identificadores que mapeiam para um dos 14 padrões que identificamos todas as contas de usuário como.

*Tabela: Identificadores de padrão de uso no mapeamento CSV exportado com padrões de uso*

| ID | 1 | 2 | 3 | 4 | 5 e 8 | 6 | 7 | 9 | 10 e 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Padrões de uso | Usuário normal | Viajante ou viajante | Família grande | Fechar família e amigos | Compartilhamento em grupo social | Grande grupo de amigos | Transmissão simultânea | Compartilhamento de comunidade | Comportamento incerto | Família pequena | Segunda página inicial | Uso anormal |

{style="table-layout:auto"}

**Probabilidade de Compartilhamento**

A probabilidade de compartilhamento é a probabilidade de que a conta específica esteja compartilhando suas credenciais.

>[!NOTE]
>
> A média da probabilidade de compartilhamento de todas as contas (no segmento selecionado) é usada para calcular a [nível de compartilhamento](/help/AccountIQ/dashboard.md#sharing-level) do [Pontuação de compartilhamento agregada](/help/AccountIQ/dashboard.md#aggregated-sharing).
