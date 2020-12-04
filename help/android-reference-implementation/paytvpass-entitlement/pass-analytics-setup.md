---
description: Você pode configurar a Implementação de referência para usar o relatórios Adobe Analytics.
seo-description: Você pode configurar a Implementação de referência para usar o relatórios Adobe Analytics.
seo-title: Configurar o Relatórios Adobe Analytics
title: Configurar o Relatórios Adobe Analytics
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Configurar o Relatórios Adobe Analytics {#configure-adobe-analytics-reporting}

Você pode configurar a Implementação de referência para usar o relatórios Adobe Analytics.

A Implementação de referência é configurada para enviar dados de evento de autenticação do Primetime para a Adobe Analytics usando a Biblioteca do Adobe Mobile incluída no SDK do Primetime. Para ativar e usar os dados de evento enviados do aplicativo, é necessário primeiro criar uma conta Adobe Analytics. Após a criação da conta:

1. Configure o aplicativo com suas informações de conta; e
1. Crie regras de processamento para personalizar como os dados do evento são exibidos em seus relatórios.

A tabela abaixo apresenta os dados enviados à Adobe Analytics:

| Nome da ação | `a.media.pass.event.MvpdSelection` | O usuário selecionou um Distribuidor de programação de vídeo de vários canais (MVPD) em uma caixa de diálogo de seleção |
|---|---|---|
| Dados de contexto | `a.media.pass.MvpdId (String)` | O MVPD selecionado pelo usuário |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |
|  |  |  |
| Nome da ação | `a.media.pass.event.AuthenticationDetection` | Um fluxo de trabalho de autenticação foi concluído |
| Dados de contexto | `a.media.pass.Successful` | (Booliano) Se a solicitação de token foi bem-sucedida, verdadeira ou falsa |
|  | `a.media.pass.MvpdId` | (String) O MVPD selecionado pelo usuário |
|  | `a.media.pass.Guid` | (String) Uma ID de rastreamento |
|  | `a.media.pass.Cached` | (Booliano) Token já em cache, verdadeiro ou falso |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |
|  |  |  |
| Nome da ação | `a.media.pass.event.AuthorizationDetection` | Fluxo de trabalho de autorização concluído |
| Dados de contexto | `a.media.pass.Successful` | (Booliano) Se a solicitação de token foi bem-sucedida, verdadeira ou falsa |
|  | `a.media.pass.MvpdId` | (String) O usuário selecionou MVPD |
|  | `a.media.pass.Guid` | (String) Uma ID de rastreamento |
|  | `a.media.pass.Cached` | (Booliano) Token já em cache, verdadeiro ou falso |
|  | `a.media.pass.Error` | (String) O erro se a tentativa de autorização falhar |
|  | `a.media.pass.ErrorDetails` | (String) Detalhes adicionais do erro |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |

1. Configure o aplicativo para uso com a Adobe Marketing Cloud.

   Para habilitar o envio de dados de autenticação Primetime Primetime à Adobe Analytics, um arquivo de configuração [!DNL `ADBMobileConfig.json`] deve ser adicionado à Implementação de referência no momento da compilação. Observe que esse é exatamente o mesmo arquivo de configuração usado pelo Primetime SDK para enviar dados do Video Analytics para o Marketing Cloud. Consulte a [documentação da Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) para obter mais informações sobre como configurar um aplicativo com sua conta da Adobe Analytics.
1. Crie regras de processamento.

   Os dados do evento de autenticação Primetime enviados pela Implementação de referência não aparecerão automaticamente nos relatórios de análise. Primeiro, você deve usar os dados criando regras de processamento. Consulte a documentação [Adobe Analytics sobre como criar regras de processamento](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
