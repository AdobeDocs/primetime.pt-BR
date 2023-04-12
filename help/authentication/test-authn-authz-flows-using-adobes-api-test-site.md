---
title: Como testar os fluxos de Autenticação e Autorização usando o site de teste API do Adobe
description: Como testar os fluxos de Autenticação e Autorização usando o site de teste API do Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Como testar os fluxos de autenticação e autorização usando o site de teste da API do Adobe {#How-to-test-auth-flows}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Para testar os fluxos AuthN e AuthZ, preparamos um **Site de teste da API** que está à sua disposição. Nossa equipe de suporte ficará feliz em fornecer credenciais. Você pode entrar em contato conosco em **support@tve.zendesk.com**.


## Parte I {#part-I}

Para testar no ambiente VERSÃO, pule diretamente para a Parte II.  Para testar no ambiente de pré-qualificação, consulte [Como configurar seu ambiente e testar no Pre-Qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

## Parte II

Após completar a parte I, execute as seguintes etapas:


1. Abrir página da Web: [Teste da API de preparo](https://sp.auth-staging.adobe.com/apitest/api.html).
1. Carregue o ativador de acesso do seguinte URL:
   * [Javascript ativador de acesso para preparo](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js).
   * OU
   * [Javascript ativador de acesso para produção](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
   * EM SEGUIDA, clique no botão **Ativador de Acesso de Carregamento** Botão &quot;.
1. Agora, defina o valor da ID do solicitante como &quot;**requestorID**&quot; e clique no botão &quot;setRequestor&quot;.
1. Depois disso, pressione o botão &quot;getAuthentication&quot; e aguarde até que o seletor de vídeo seja exibido.
1. Selecione o &quot;**MVPD**&quot; do selecionador.
1. Insira suas credenciais no &quot;**MVPD**&quot; página de logon.
1. Depois de ser redirecionado, refaça as etapas de 1 a 3
1. Depois de refazer a etapa 3 no &quot;setAuthenticationStatus&quot;, você deve ver o valor &quot;1&quot;. Se a autenticação não funcionou, a caixa de diálogo MVPD será exibida.
1. Para testar a autorização, no campo de entrada de recursos, digite &quot;**requestorID**&quot; e clique no botão &quot;getAuthorization&quot;.
1. Como resultado, na caixa de texto &quot;setToken&quot;-\> &quot;resource id&quot;, o recurso será exibido e, na caixa de texto &quot;setToken&quot;-\> &quot;token&quot;, o shortAuthorizationToken será mostrado, significando que authZ foi bem-sucedido.
1. Agora é possível clicar no botão &quot;logout&quot; para excluir os tokens.

