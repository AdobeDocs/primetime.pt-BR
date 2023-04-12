---
title: Integração dos dados do lado do servidor de autenticação do Primetime ao Adobe Analytics
description: Integração dos dados do lado do servidor de autenticação do Primetime ao Adobe Analytics
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 4%

---


# Integração dos dados do lado do servidor da Autenticação do Primetime ao Adobe Analytics

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Os clientes da Autenticação do Adobe Primetime desejam ver os dados do lado do servidor da autenticação do Primetime (Adobe Pass) no painel do Adobe Analytics para facilitar o consumo.

Os dados servirão para rastrear métricas TVE importantes, como taxas de conversão de autenticação por MVPD, usuários exclusivos com base na ID de usuário do MVPD e muito mais.

Não se destina a substituir uma implementação do lado do cliente se já existir, pois a atividade do usuário não pode ser rastreada além dos eventos específicos abaixo, na ausência de uma ID de visitante. Se os clientes estiverem fornecendo uma ID de visitante em chamadas Pass , poderemos desbloquear outro tipo de integração do Analytics - em tempo real - que pode associar todos os eventos Pass com os dados do cliente existente, mais detalhes sobre esse novo tipo de integração possível aqui: &quot;[Uso de Experience Cloud ID na autenticação do Primetime](/help/authentication/exp-cloud-id-authn.md)&quot;

## Métricas incluídas {#metrics-included-int-authn-analyt}

| Evento | Descrição |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| AuthN solicitado | Número de fluxos de autenticação iniciados |
| AuthN pendente | Número de tokens de autenticação gerados com êxito (ignorando se o cliente realmente os obteve ou não) |
| AuthN OK | Número de tokens de autenticação obtidos com êxito pelos usuários |
| AuthZ solicitado | Número de autorizações tentadas |
| AuthZ OK | Número de autorizações bem-sucedidas |
| Falha de AuthZ | Número de autorizações negadas por MVPD a nível de aplicação |
| Reproduzir solicitação | Número de tokens de mídia curtos gerados (que se assimilam ao número de solicitações de reprodução) |
| Logout solicitado | Número de fluxos de logout iniciados |
| Logout concluído | Número de fluxos de logout concluídos com êxito |
| Falha no logout | Número de fluxos de logout com falha |
| Pré-autorização solicitada | Número de fluxos de pré-autorização iniciados |
| Pré-autorização OK | Número de eventos de pré-autorização bem-sucedidos com os recursos que foram pré-autorizados |
| Pré-autorização negada | Número de eventos de pré-autorização com os recursos aos quais foi negada pré-autorização |
| Falha na pré-autorização | Número de eventos de pré-autorização que falharam |

| Nome do Adobe Analytics | Descrição |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Canal | A ID do solicitante usada para executar a solicitação de direito |
| MVPD | O MVPD responsável pela concessão do direito ao usuário |
| Proxy | O MVPD proxy (que será &quot;Direto&quot; para integrações diretas) |
| Tipo de SDK | O SDK do cliente usado (Flash, HTML5, Android nativo, iOS, sem cliente etc.) |
| Versão do SDK | A versão do SDK do cliente de autenticação da Adobe Primetime |
| ID do recurso | O título real do recurso envolvido no pedido de autorização (extraído da carga do MRSS como o item/título, se fornecido) |
| Tipo de erro AuthZ | O motivo das falhas, conforme relatado pela autenticação da Adobe Primetime <br/> Estes são os valores mais comuns <br/> **noAuthZ** = o MVPD respondeu que o usuário não tem o canal em seu pacote<br/> **rede** = não foi possível alcançar o MVPD (o MVPD tem um problema no momento da chamada e não respondeu)<br/> **norefreshtoken** = é estritamente para implementações OAuth e pode resultar se o usuário alterar sua senha ou se o MVPD a negou por algum motivo. Geralmente resulta em uma nova autenticação<br/> **incompatibilidade** = se a solicitação for feita de um dispositivo diferente daquele que tinha o token de autenticação. Pode resultar se os usuários tentarem enganar o sistema, mas a maioria desses eventos aconteceu no contexto de nosso SDK JavaScript antigo, onde a ID do dispositivo estava usando o endereço IP como parte do cálculo. Se um usuário assistisse TVE em casa e depois no trabalho, esse erro seria acionado e ele precisaria autenticar novamente<br/> **inválido** = solicitação inválida, parâmetros ausentes ou inválidos<br/>  **authzNone** = Os programadores têm a capacidade de negar autorizações para uma combinação específica de channelMVPD. Isso é acionado por uma API de back-end à qual os programadores têm acesso<br/> **fraude** = é um mecanismo de proteção do nosso lado. Se o usuário falhar na autorização e, em seguida, a solicitar novamente várias vezes em um curto intervalo (segundos), a chamada será negada diretamente. Normalmente, isso acontece quando um Programador tem um bug em sua implementação que solicita autorização constantemente se falhar. |
| Tipo de token | Quando os tokens são criados devido a AuthZ All e AuthN All, precisamos saber o que é causado por uma medida de degradação.<br/> Eles são:<br/> &quot;normal&quot; = o caso normal<br/> &quot;authnall&quot; = Quando AuthN All está ativado<br/> &quot;authzall&quot; = Quando AuthZ All está ativado<br/>  &quot;hba&quot; = Quando o HBA está ativado |
| Tipo de dispositivo sem cliente | A plataforma do dispositivo (alternativa), usada atualmente para sem cliente.<br/> Os valores podem ser:<br/> N/A - o evento não foi originado de um SDK sem cliente<br/> Desconhecido - desde que o parâmetro deviceType de um **API sem cliente** for opcional, há chamadas que não contêm nenhum valor.<br/> Qualquer outro valor enviado por meio da variável **API sem cliente**. Por exemplo, xbox, appletv e roku. |
| ID de usuário do MVPD | Substitui a ID de visitante baseada em cookie |


## Detalhes {#details-int-authn-analyt}

* As métricas serão inseridas, evento por evento no conjunto de relatórios específico por meio da API de inserção de dados do Adobe Analytics
* A inserção será armazenada em lote e enviada a cada 30 minutos. Devido a isso, o relatório precisa ter um carimbo de data e hora
* Cada cliente terá um ou vários conjuntos de relatórios. Uma ID de solicitante (canal) mapeará somente para um conjunto de relatórios. Várias IDs de solicitante podem mapear para apenas um conjunto de relatórios.
* Os dados históricos podem ser fornecidos, mas será necessário ter cuidado especial devido a preocupações de tráfego/desempenho.
* A variável de visitante único é definida como ID de usuário MVPD
* O mapeamento de eventos e eVars não pode ser configurado.


## SLA {#sla-int-authn-serv-anal}

Como não é um componente crítico, não há garantia de SLA para a integração.

## Configuração do conjunto de relatórios {#report-suite-config}

O relatório deve ter um carimbo de data e hora, pois os eventos serão enviados em lotes.

### Eventos {#report-suite-config-events}


>[!NOTE]
>Todos devem ser definidos com:
>
>* Contador (sem sub-relações)


| Evento | Evento Adobe Analytics |
|---------------------------------------|-----------------------|
| AuthN solicitado | event1 |
| AuthN pendente | event2 |
| AuthN OK | event3 |
| AuthZ solicitado | event4 |
| AuthZ OK | event5 |
| Falha de AuthZ | event6 |
| Reproduzir solicitação | event7 |
| Falha de AuthN | event8 |
| Solicitação de Token AuthN sem cliente OK | event9 |
| Falha na Solicitação de Token AuthN sem Cliente | event10 |
| Falha na reprodução da solicitação | event11 |
| Solicitação de logout | event12 |
| Logout concluído | event13 |
| Falha no logout | event14 |
| Solicitação de comprovação | event15 |
| Falha na comprovação | event16 |
| Pré-visualização concedida | event17 |
| Pré-visualização negada | event18 |


### eVars {#evars}


>[!NOTE]
>Todos devem ser definidos com:
>
>* Alocação: Mais recente (último)
>* Expirar após: Ocorrência
>* Tipo: String de texto


| Propriedade | eVar |
|-----------------------------------|--------------------------------|
| Canal | eVar1 |
| MVPD | eVar2 |
| Proxy | eVar3 |
| Tipo de SDK | eVar4 |
| Versão do SDK | eVar5 |
| ID do recurso | eVar6 |
| Tipo de erro AuthZ | eVar7 |
| Tipo de token | eVar8 |
| Tipo de dispositivo sem cliente | eVar9 |
| ID de usuário do MVPD | visitorID (feito automaticamente) |
| ID de usuário do MVPD | eVar10 |
| Tipo de dispositivo | eVar11 |
| Sistema operacional | eVar12 |
| Tipo de hardware principal | eVar13 |
| TTL | eVar14 |
| Tipo de autenticação | eVar15 |
| Versão da arquitetura do servidor | eVar16 |
| Provedor de autenticação externo | eVar17 |
| Latência | eVar18 |
| Id Do Visitante | eVar19 |
| Mecanismo SSO | eVar20 |
| Modelo do dispositivo | eVar21 |
| Versão do dispositivo | eVar22 |
| Modelo de hardware do dispositivo | eVar23 |
| Fornecedor de hardware do dispositivo | eVar24 |
| Fabricante de hardware do dispositivo | eVar25 |
| Versão do hardware do dispositivo | eVar26 |
| Nome do SO do dispositivo | eVar27 |
| Família do SO do dispositivo | eVar28 |
| Fornecedor do SO do dispositivo | eVar29 |
| Versão do SO do dispositivo | eVar30 |
| Nome do navegador do dispositivo | eVar31 |
| Fornecedor do navegador de dispositivos | eVar32 |
| Versão do navegador do dispositivo | eVar33 |
| Tipo de dispositivo sem cliente normalizado | eVar34 |

## Preços {#pricing}

Entre em contato com a TAM para obter mais informações.
