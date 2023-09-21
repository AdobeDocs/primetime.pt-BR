---
description: Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.
title: Configurar relatórios do Adobe Analytics
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Configurar relatórios do Adobe Analytics {#configure-adobe-analytics-reporting}

Você pode configurar a Implementação de referência para usar os relatórios do Adobe Analytics.

A Implementação de referência é configurada para enviar dados do evento de autenticação do Primetime para a Adobe Analytics usando a Biblioteca móvel do Adobe fornecida no SDK do Primetime. Para habilitar e usar os dados do evento enviados do aplicativo, primeiro crie uma conta do Adobe Analytics. Depois que a conta for criada:

1. Configurar o aplicativo com as informações da sua conta; e
1. Crie regras de processamento para personalizar como os dados do evento são exibidos em seus relatórios.

A tabela abaixo apresenta os dados enviados para o Adobe Analytics:

| Nome da ação | `a.media.pass.event.MvpdSelection` | O usuário selecionou um Distribuidor de programação de vídeo multicanal (MVPD) em um diálogo de seleção |
|---|---|---|
| Dados de contexto | `a.media.pass.MvpdId (String)` | O MVPD selecionado pelo usuário |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |
|  | | |
| Nome da ação | `a.media.pass.event.AuthenticationDetection` | Um fluxo de trabalho de autenticação foi concluído |
| Dados de contexto | `a.media.pass.Successful` | (Booleano) Se a solicitação de token foi bem-sucedida, verdadeira ou falsa |
|  | `a.media.pass.MvpdId` | (String) O MVPD selecionado pelo usuário |
|  | `a.media.pass.Guid` | (String) Uma ID de rastreamento |
|  | `a.media.pass.Cached` | (Booleano) Token já em cache, verdadeiro ou falso |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |
|  | | |
| Nome da ação | `a.media.pass.event.AuthorizationDetection` | Um fluxo de trabalho de autorização foi concluído |
| Dados de contexto | `a.media.pass.Successful` | (Booleano) Se a solicitação de token foi bem-sucedida, verdadeira ou falsa |
|  | `a.media.pass.MvpdId` | (String) O MVPD selecionado pelo usuário |
|  | `a.media.pass.Guid` | (String) Uma ID de rastreamento |
|  | `a.media.pass.Cached` | (Booleano) Token já em cache, verdadeiro ou falso |
|  | `a.media.pass.Error` | (String) O erro se a tentativa de autorização falhar |
|  | `a.media.pass.ErrorDetails` | (String) Mais detalhes do erro |
|  | `a.media.pass.ClientType` | (String) O tipo de cliente como &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; ou &quot;android&quot; |

1. Configure o aplicativo para ser usado com o Adobe Marketing Cloud.

   Para habilitar o envio de dados de autenticação do Primetime para o Adobe Analytics, um [!DNL `ADBMobileConfig.json`] O arquivo de configuração deve ser adicionado à Implementação de referência no momento da compilação. Observe que esse é exatamente o mesmo arquivo de configuração usado pelo SDK do Primetime para enviar dados do Video Analytics para o Marketing Cloud. Consulte o [Documentação do Adobe Marketing Cloud](https://microsite.omniture.com/t2/help/en_US/reference/) para obter mais informações sobre como configurar um aplicativo com sua conta do Adobe Analytics.
1. Criar regras de processamento.

   Os dados do evento de autenticação do Primetime enviados pela Implementação de referência não aparecerão automaticamente nos relatórios de análise. Primeiro, você deve usar os dados criando regras de processamento. Consulte o [Documentação do Adobe Analytics sobre criação de regras de processamento](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
