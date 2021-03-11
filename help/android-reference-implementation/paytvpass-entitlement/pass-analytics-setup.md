---
description: Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.
title: Configurar relatórios do Adobe Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# Configurar relatórios do Adobe Analytics {#configure-adobe-analytics-reporting}

Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.

A Implementação de referência é configurada para enviar dados de evento de autenticação do Primetime para o Adobe Analytics usando a Biblioteca para dispositivos móveis do Adobe fornecida no SDK do Primetime. Para habilitar e usar os dados do evento enviados do aplicativo, primeiro crie uma conta Adobe Analytics . Depois que a conta é criada:

1. Configure o aplicativo com suas informações de conta; e
1. Crie regras de processamento para personalizar como os dados do evento são exibidos em seus relatórios.

A tabela abaixo apresenta os dados enviados para a Adobe Analytics:

| Nome da ação | `a.media.pass.event.MvpdSelection` | O usuário selecionou um Distribuidor de Programação de Vídeo Multicanal (MVPD) em uma caixa de diálogo de seleção |
|---|---|---|
| Dados de contexto | `a.media.pass.MvpdId (String)` | O MVPD selecionado pelo usuário |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |
|  |  |  |
| Nome da ação | `a.media.pass.event.AuthenticationDetection` | Um fluxo de trabalho de autenticação foi concluído |
| Dados de contexto | `a.media.pass.Successful` | (Booleano) Se a solicitação de token foi bem-sucedida, verdadeira ou falsa |
|  | `a.media.pass.MvpdId` | (Cadeia de caracteres) O MVPD selecionado pelo usuário |
|  | `a.media.pass.Guid` | (String) Uma ID de rastreamento |
|  | `a.media.pass.Cached` | (Booleano) Token já em cache, verdadeiro ou falso |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |
|  |  |  |
| Nome da ação | `a.media.pass.event.AuthorizationDetection` | Um fluxo de trabalho de autorização foi concluído |
| Dados de contexto | `a.media.pass.Successful` | (Booleano) Se a solicitação de token foi bem-sucedida, verdadeira ou falsa |
|  | `a.media.pass.MvpdId` | (Cadeia de caracteres) O usuário selecionou MVPD |
|  | `a.media.pass.Guid` | (String) Uma ID de rastreamento |
|  | `a.media.pass.Cached` | (Booleano) Token já em cache, verdadeiro ou falso |
|  | `a.media.pass.Error` | (String) O erro se a tentativa de autorização falhar |
|  | `a.media.pass.ErrorDetails` | (String) Mais detalhes do erro |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |

1. Configure o aplicativo para uso com o Adobe Marketing Cloud.

   Para habilitar o envio de dados de autenticação do Primetime Primetime para o Adobe Analytics, um arquivo de configuração [!DNL `ADBMobileConfig.json`] deve ser adicionado à Implementação de referência no momento da compilação. Observe que esse é exatamente o mesmo arquivo de configuração usado pelo SDK do Primetime para enviar dados do Video Analytics para o Marketing Cloud. Consulte a [documentação do Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) para obter mais informações sobre como configurar um aplicativo com sua conta do Adobe Analytics.
1. Criar regras de processamento.

   Os dados do evento de autenticação do Primetime enviados pela Implementação de referência não serão exibidos automaticamente em seus relatórios de análise. Primeiro, você deve usar os dados criando regras de processamento. Consulte a documentação do [Adobe Analytics sobre como criar regras de processamento](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
