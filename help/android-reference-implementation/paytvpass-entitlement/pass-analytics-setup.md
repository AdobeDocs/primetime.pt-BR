---
description: Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.
seo-description: Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.
seo-title: Configurar relatórios do Adobe Analytics
title: Configurar relatórios do Adobe Analytics
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Configurar relatórios do Adobe Analytics {#configure-adobe-analytics-reporting}

Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.

A Implementação de referência é configurada para enviar dados de eventos de autenticação Primetime para o Adobe Analytics usando a Biblioteca do Adobe Mobile incluída no SDK do Primetime. Para ativar e usar os dados de evento enviados do aplicativo, é necessário primeiro criar uma conta do Adobe Analytics. Após a criação da conta:

1. Configure o aplicativo com suas informações de conta; e
1. Crie regras de processamento para personalizar como os dados do evento são exibidos em seus relatórios.

A tabela abaixo apresenta os dados enviados para o Adobe Analytics:

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

   Para habilitar o envio de dados de autenticação Primetime Primetime ao Adobe Analytics, um arquivo de [!DNL `ADBMobileConfig.json`] configuração deve ser adicionado à Implementação de referência no momento da compilação. Observe que esse é exatamente o mesmo arquivo de configuração usado pelo Primetime SDK para enviar dados do Video Analytics para a Marketing Cloud. Consulte a documentação [da](https://microsite.omniture.com/t2/help/en_US/reference/) Adobe Marketing Cloud para obter mais informações sobre como configurar um aplicativo com sua conta do Adobe Analytics.
1. Crie regras de processamento.

   Os dados do evento de autenticação Primetime enviados pela Implementação de referência não aparecerão automaticamente nos relatórios de análise. Primeiro, você deve usar os dados criando regras de processamento. Consulte a documentação do [Adobe Analytics para obter informações sobre como criar regras](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html)de processamento.
