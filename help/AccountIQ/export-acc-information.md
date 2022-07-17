---
title: Exportar informações para contas com pontuação de compartilhamento alta
description: Exportar informações para contas com pontuação de compartilhamento alta.
source-git-commit: 17a44bde5cf320f519cc537d37df0fe823cf51a6
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---


# Exportar informações para contas com pontuação de compartilhamento alta {#export-account-info-high-score}

O Account IQ oferece a opção de exportar detalhes de compartilhamento de conta para as 1000 contas de assinante principais com base em suas [compartilhando probabilidades](/help/AccountIQ/product-concepts.md#account-sharing-probability-def). Os dados no arquivo CSV exportado são classificados na ordem decrescente das probabilidades de compartilhamento das contas do assinante - dos MVPDs selecionados na variável [segmento](/help/AccountIQ/product-concepts.md#segment-def)para um [período especificado](/help/AccountIQ/product-concepts.md#time-frame-def).

A opção para exportar as informações de compartilhamento de conta está disponível em [Relatórios de uso geral](/help/AccountIQ/general-usage-reports.md) e [Relatórios de contas compartilhadas](/help/AccountIQ/shared-acc-reports.md) páginas.

>[!NOTE]
>
>Os números no arquivo CSV baixado são diferentes para as páginas de relatórios de Uso geral e Contas compartilhadas . Isso ocorre porque a página Relatórios de uso geral tem filtros adicionais para os programadores selecionarem Limite para número de dispositivos, IPs e CEPs. Portanto, os dados exportados dos relatórios de Uso geral são baseados no filtro de limite adicional aplicado.

![Opção Exportar em uso Geral](assets/export.png)

Para exportar as informações de compartilhamento de conta dos assinantes:

1. Especifique um segmento no seletor de segmentos. Para selecionar um segmento:

   1. Selecione os MVPDs desejados de **MVPDs no segmento** opção.

   1. Selecione os Canais desejados em **Canais no segmento** opção.

   1. Selecione um período de tempo de **Granularidade e período** para exibir relatórios para isso.

1. Selecione o **Exportar as 1000 contas principais** opção para exportar as informações da conta para 1000 assinantes com maior probabilidade de compartilhamento.

Ao usar a opção de exportação, as estatísticas para 1000 contas com as maiores probabilidades de compartilhamento (para um período de tempo definido) são baixadas para a pasta Downloads da máquina local.

>[!NOTE]
>
>O arquivo CSV baixado pode ser aberto usando qualquer aplicativo que leia o arquivo CSV, por exemplo, Microsoft Excel.

![dados exportados no formato csv](assets/exported-csv.png)

*Figura: Dados de conta compartilhada exportados no formato CSV*

## Colunas no relatório exportado {#columns-in-export}

**Semana/Mês**

A semana ou o mês selecionado no **Granularidade e intervalo de tempo** no seletor de segmentos, para o qual as estatísticas de compartilhamento são buscadas.

**MVPD**

Se você for um usuário programador, a coluna mostra a qual MVPD a conta do assinante pertence.

**ID do assinante**

Conta específica de que estamos a falar em seguida.

**Número mínimo de dispositivos**

O número real de dispositivos (esse conteúdo de fluxo) é quase certamente maior do que o número mínimo de dispositivos, especificado para uma conta específica.

>[!NOTE]
>
>O número real de dispositivos (esse conteúdo de fluxo) é certamente maior que o Número mínimo de dispositivos, especificado para uma conta específica.

**Número mínimo de pessoas**

O número mínimo absoluto de pessoas que eram conteúdo de transmissão ativo usando esses dispositivos.

>[!NOTE]
>
>O número real de pessoas (esse conteúdo de fluxo) é quase certamente muito maior do que o Número Mínimo de pessoas, especificado para uma conta específica.

**# IPs**

Número de endereços IP a partir dos quais o conteúdo é transmitido.

**# Localizações**

Número de locais (com base no código postal) a partir dos quais o conteúdo é transmitido.

**# Cidades**

Número de cidades onde o streaming aconteceu.

**# Estados**

Número de estados em que o streaming ocorreu.

**# Clusters**

O número de distintos [clusters](/help/AccountIQ/product-concepts.md#cluster-def) onde o streaming aconteceu.

**Extensão geográfica (milhas)**

A distância máxima entre os locais de transmissão associados à conta.

**# AuthN OK**

O número de vezes que os usuários fizeram logon durante o período, usando essa conta.

**# AuthZ OK**

Número de vezes que um MVPD autorizou um fluxo ou concedeu acesso (ao conteúdo) a essa conta.

>[!NOTE]
>
>O **# AuthZ OK** está relacionada ao **Nº de Solicitações de Reprodução**; é menor que a variável **Nº de Solicitações de Reprodução** porque o Adobe armazena em cache as autorizações fornecidas para os MVPDs normalmente durante 24 horas.

**Nº de Solicitações de Reprodução**

O número real de fluxos durante o período de tempo.

**# Canais**

Número total de canais diferentes que a conta assistiu ao longo do período.

>[!NOTE]
>
>**# Canais** inclui os canais que não pertenciam necessariamente ao programador conectado.
>
>Esse número para a conta foi exibido porque a conta assistiu ao canal, mas também acessou outros canais durante esse período.

**Padrão de uso**

Os números nesta coluna são identificadores que mapeiam para um dos 14 padrões que identificamos todas as contas de usuário como.

*Tabela: Identificadores de padrão de uso no mapeamento CSV exportado com padrões de uso*

| ID | 1 | 2 | 3 | 4 | 5 e 8 | 6 | 7 | 9 | 10 e 11 | 12º | 13º | 14. |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Padrões de uso | Usuário regular | Viajante ou viajante | Família Grande | Família e amigos próximos | Compartilhamento em grupo social | Grande grupo de amigos | Streaming simultâneo | Compartilhamento da comunidade | Comportamento incerto | Pequena família | Segunda casa | Uso anormal |

{style=&quot;table-layout:auto&quot;}

**Probabilidade de compartilhamento**

A probabilidade de compartilhamento é a probabilidade de a conta específica estar compartilhando suas credenciais.

>[!NOTE]
>
> A média da probabilidade de compartilhamento de todas as contas (no segmento selecionado) é usada para calcular a variável [nível de compartilhamento](/help/AccountIQ/dashboard.md#sharing-level) do [Pontuação de compartilhamento agregada](/help/AccountIQ/dashboard.md#aggregated-sharing).
