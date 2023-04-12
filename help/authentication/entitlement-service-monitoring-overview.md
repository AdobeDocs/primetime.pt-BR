---
title: Visão geral do monitoramento do serviço de direito
description: Visão geral do monitoramento do serviço de direito
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Visão geral do monitoramento do serviço de direito {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#introduction}

Os sites e aplicativos TVE precisam estar disponíveis 24 horas por dia, 7 dias por semana, de modo que os clientes exigem um insight em tempo real sobre os eventos de direito para detectar e corrigir problemas o mais rápido possível. Eles também precisam analisar dados mensais para determinar quais plataformas estão fornecendo a maior parte do tráfego e quais plataformas podem ter uma implementação ruim e taxas de conversão baixas.

O ESM (Entitlement Service Monitoring) fornece aos programadores e MVPDs um feed de dados que oferece visibilidade em tempo real aos eventos de Autenticação e Autorização. Os dados são coletados dos sistemas de autenticação da Adobe Primetime e fornecidos por meio de uma RESTful API.  Os clientes podem consumir os dados diretamente ou de dentro de seus próprios painéis operacionais personalizados.

Os elementos principais do sistema ESM são suas métricas e dimensões. O ESM gera relatórios que contêm métricas agregadas de acordo com a seleção de dimensão. Como os eventos Adobe Pass são registrados no fuso horário PST, os relatórios ESM também estão disponíveis no fuso horário PST. 

A API ESM geralmente não está disponível.  Entre em contato com seu representante de Adobe para obter perguntas sobre disponibilidade.

## ESM para programadores {#esm-for-programmers}

### Os programadores podem monitorar as seguintes métricas: {#programmers-monitor-metrics}


| *Nome das métricas* | *Descrição* |
|-------------------------|--------------------------|
| authn-tries | Número de fluxos de autenticação iniciados |
| authn-success | Número de tokens de autenticação obtidos com êxito pelos clientes |
| aun-pending | Número de tokens de autenticação gerados com êxito (ignorando se o cliente realmente os obteve ou não) |
| authn-failed | Número de autenticação com falha realizada por meio de um sistema externo. |
| clientless-tokens | Número de tokens sem cliente emitidos com êxito |
| clientless-failure | Número de tentativas com falha para receber tokens da API sem cliente |
| authz-tries | Número de autorizações tentadas |
| authz-success | Número de autorizações bem-sucedidas |
| authz-failed | Número de autorizações negadas por MVPD a nível de aplicação |
| authz-rejected | Número de tentativas de autorização consideradas maliciosas pelo Provedor de serviços da Adobe e rejeitadas como resultado de uma prevenção de ataque doS |
| authz-latency | Número total de milissegundos gastos no terminal do MVPD |
| media-tokens | Número de tokens de mídia curtos gerados (que se assimilam ao número de solicitações de reprodução) |
| contas exclusivas | Número de usuários únicos que executaram ações de direito (AuthN / AuthZ) no intervalo de tempo selecionado. (Essa métrica só mostrará se os valores diários forem solicitados.) </br> Isso é calculado para cada data center individual. Quando a dimensão &quot;dc&quot; não for solicitada, essa métrica não será exibida. |
| sessões exclusivas | Número de sessões exclusivas que executaram chamadas de fluxo de autenticação para o serviço de autenticação da Adobe Primetime no intervalo de tempo selecionado. (Essa métrica só mostrará se os valores diários forem solicitados.) </br> Isso é calculado para cada data center individual. Quando a dimensão &quot;dc&quot; não for solicitada, essa métrica não será exibida. |
| count | Um contador simples usado nos relatórios orientados para o evento |

</br>

### Os programadores podem filtrar as métricas listadas acima pelas seguintes dimensões: {#progr-filter-metrics}


| *Nome do Dimension* | *Descrição* |
|---|---|
| ano | Ano de 4 dígitos |
| mês | O mês do ano (1-12) |
| dia | O dia do mês (1-31) |
| hour | A hora do dia |
| minuto | O minuto da hora |
| empresa de mídia | A empresa de mídia proprietária do site que iniciou o processo de direito do usuário |
| dc | (Centro de dados) A região inicial onde a solicitação foi recebida. |
| proxy | O MVPD proxy (que será &quot;Direto&quot; para integrações diretas) |
| mvpd | O MVPD responsável pela concessão do direito ao usuário |
| requestor-id | A ID do solicitante usada para executar a solicitação de direito |
| canal | O site do canal, extraído do campo de recurso (extraído da carga MRSS como canal/título, se fornecido, ou mapeado para o valor do recurso, se não estiver no formato RSS). |
| resource-id | O título real do recurso envolvido no pedido de autorização (extraído da carga do MRSS como o item/título, se fornecido) |
| dispositivo | A plataforma do dispositivo (PC, móvel, console etc.) |
| mapa | O provedor de autenticação externo quando o fluxo de autenticação é executado por um sistema externo. </br> Os valores podem ser: </br> - N/A - a autenticação foi fornecida pela autenticação do Primetime </br> - Apple - o sistema externo que forneceu a autenticação é o Apple |
| os-family | Sistema operacional em execução no dispositivo |
| família de navegadores | Agente do usuário usado para acessar a autenticação da Adobe Primetime |
| cdt | A plataforma do dispositivo (alternativa), usada atualmente para sem cliente. </br>  Os valores podem ser: </br> - N/A - o evento não foi originado de um SDK sem cliente </br> - Desconhecido - Como o parâmetro deviceType de uma API sem cliente é opcional, há chamadas que não contêm valor. </br> - qualquer outro valor enviado por meio da API sem cliente, por exemplo, xbox, appletv, roku etc. </br> |
| platform-version | A versão do SDK sem cliente |
| os-type | Sistema operacional em execução no dispositivo, alternativo (não usado no momento) |
| versão do navegador | Versão do agente do usuário |
| tipo sdk | O SDK do cliente usado (Flash, HTML5, Android nativo, iOS, sem cliente etc.) |
| sdk-version | A versão do SDK do cliente de autenticação da Adobe Primetime |
| evento | O nome do evento de autenticação da Adobe Primetime |
| reason | O motivo das falhas, conforme relatado pela autenticação da Adobe Primetime |
| sso-type | O mecanismo de SSO subjacente: platform/passive/adobe. Indica que o token de autorização foi emitido reutilizando o AuthN num pedido diferente |

## ESM para MVPDs {#esm-for-mvpds}

### Os MVPDs podem monitorar as seguintes métricas:

| *Nome da métrica* | *Descrição* |
|---|---|
| authn-tries | Número de fluxos de autenticação iniciados |
| authn-success | Número de tokens de autenticação obtidos com êxito pelos clientes |
| aun-pending | Número de tokens de autenticação gerados com êxito (ignorando se o cliente realmente os obteve ou não) |
| authn-failed | Número de autenticação com falha realizada por meio de um sistema externo. |
| authz-tries | Número de autorizações tentadas |
| authz-success | Número de autorizações bem-sucedidas |
| authz-failed | Número de autorizações negadas por MVPD a nível de aplicação |
| authz-rejected | Número de tentativas de autorização consideradas maliciosas pelo Provedor de serviços da Adobe e rejeitadas como resultado de uma prevenção de ataque doS |
| authz-latency | Número total de milissegundos gastos no terminal do MVPD |

### Os MVPDs podem filtrar as métricas listadas acima pelas seguintes dimensões:

| *Nome do Dimension* | *Descrição* |
|---|---|
| ano | Ano de 4 dígitos |
| mês | O mês do ano (1-12) |
| dia | O dia do mês (1-31) |
| hour | A hora do dia |
| minuto | O minuto da hora |
| requestor-id | A ID do solicitante usada para executar a solicitação de direito |
| mapa | O provedor de autenticação externo quando o fluxo de autenticação é executado por um sistema externo. </br> Os valores podem ser: </br> - N/A - a autenticação foi fornecida pela autenticação do Primetime </br> - Apple - o sistema externo que forneceu a autenticação é o Apple |
| cdt | A plataforma do dispositivo (alternativa), usada atualmente para sem cliente. </br>  Os valores podem ser: </br> - N/A - o evento não foi originado de um SDK sem cliente </br> - Desconhecido - Como o parâmetro deviceType de uma API sem cliente é opcional, há chamadas que não contêm valor. </br> - qualquer outro valor enviado por meio da API sem cliente, por exemplo, xbox, appletv, roku etc. </br> |
| tipo sdk | O SDK do cliente usado (Flash, HTML5, Android nativo, iOS, sem cliente etc.) |


## Casos de uso {#use-cases}

Você pode usar os dados ESM para os seguintes casos de uso:

- **Monitoramento** - As equipes de monitoramento ou de operações podem criar um painel ou gráfico que chama a API a cada minuto. Usando as informações exibidas, é possível detectar um problema (com a autenticação do Primetime ou com um MVPD) no minuto que ele for exibido.  

- **Depuração/Teste de qualidade** - Como os dados também são detalhados por plataforma, dispositivo, navegador e SO, a análise de padrões de uso pode identificar problemas em combinações específicas (por exemplo, Safari no OSX).  

- **Analytics** - Os dados fornecidos podem ser usados para complementar/auditar os dados do lado do cliente que estão sendo coletados por meio do Adobe Analytics ou de outra ferramenta de análise.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->