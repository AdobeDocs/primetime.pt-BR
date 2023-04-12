---
title: Guia de integração do Amazon FireOS
description: Guia de integração do Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---


# Guia de integração do Amazon FireOS {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>


## Introdução {#intro}

Este documento descreve os workflows de direito que um aplicativo de nível superior do Programador pode implementar por meio das APIs expostas pela biblioteca Amazon FireOS AccessEnabler.

A solução de direito de autenticação da Adobe Primetime para o Amazon FireOS é dividida em dois domínios:

- O domínio da interface do usuário: essa é a camada de aplicativo de nível superior que implementa a interface do usuário e usa os serviços fornecidos pela biblioteca AccessEnabler para fornecer acesso a conteúdo restrito.
- O domínio AccessEnabler - é aqui que os workflows de direito são implementados no formato de:
   - Chamadas de rede feitas para servidores backend do Adobe
   - Regras de lógica de negócios relacionadas aos workflows de autenticação e autorização
   - Gerenciamento de vários recursos e processamento do estado do workflow (como o cache de tokens)

O objetivo do domínio AccessEnabler é ocultar todas as complexidades dos workflows de direito e fornecer ao aplicativo de camada superior (por meio da biblioteca AccessEnabler) um conjunto de primitivos de direito simples com os quais você implementa os workflows de direito:

1. Definir a identidade do solicitante
1. Verificar e obter autenticação em relação a um determinado provedor de identidade
1. Verificar e obter autorização para um recurso específico
1. Logout

A atividade de rede do AccessEnabler ocorre em um thread diferente para que o thread da interface do usuário nunca seja bloqueado. Como resultado, o canal de comunicação bidirecional entre os dois domínios de aplicativos deve seguir um padrão totalmente assíncrono:

- A camada do aplicativo da interface do usuário envia mensagens para o domínio AccessEnabler por meio das chamadas de API expostas pela biblioteca AccessEnabler .
- O AccessEnabler responde à camada da interface do usuário por meio dos métodos de retorno de chamada incluídos no protocolo AccessEnabler, que a camada da interface do usuário registra na biblioteca AccessEnabler .

## Fluxos de direito {#entitlement}

1. [Pré-requisitos](#prereqs)
1. [Fluxo de inicialização](#startup_flow)
1. [Fluxo de autenticação](#authn_flow)
1. [Fluxo de autorização](#authz_flow)
1. [Exibir fluxo de mídia](#media_flow)
1. [Fluxo de logout](#logout_flow)

 

### A. Pré-requisitos {#prereqs}

1. Crie suas funções de retorno de chamada:
   - [`setRequestorComplete()`](#$setRequestorComplete)

      - Disparado por `setRequestor()`, retorna bem-sucedido ou falha.     Sucesso indica que você pode continuar com chamadas de direito.
   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      - Disparado por `getAuthentication()` somente se o usuário não tiver selecionado um provedor (MVPD) e ainda não tiver sido autenticado. O `mvpds` é uma matriz de provedores disponíveis para o usuário.
   - [`setAuthenticationStatus(status, motivo)`](#$setAuthNStatus)

      - Disparado por `checkAuthentication()` sempre. Disparado por `getAuthentication()` somente se o usuário já estiver autenticado e tiver selecionado um provedor.

      - O status retornado é autenticado ou não está autenticado, o motivo descreve uma falha de autenticação ou uma ação de logout.
   - [navigateToUrl(url)](#$navigateToUrl)

      - Ignorado no SDK do AmazonFireOS, o método é usado em plataformas Android, onde é acionado por `getAuthentication()` depois que o usuário seleciona um MVPD.  O `url` fornece o local da página de logon do MVPD.
   - [`sendTrackingData(event, data)`](#$sendTrackingData)

      - Disparado por `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
O `event` indica qual evento de direito ocorreu; o parâmetro `data` é uma lista de valores relacionados ao evento. 
   - [`setToken(token, recurso)`](#$setToken)

      - Disparado por `checkAuthorization()` e `getAuthorization()` após uma autorização bem-sucedida para visualizar um recurso.
      - O `token` é o token de mídia de curta duração; o parâmetro `resource` é o conteúdo que o usuário está autorizado a visualizar.
   - [`tokenRequestFailed(recurso, código, descrição)`](#$tokenRequestFailed)

      - Disparado por `checkAuthorization()` e `getAuthorization()` após uma autorização infrutífera.
      - O `resource` é o conteúdo que o usuário estava tentando visualizar; o `code` é o código de erro que indica o tipo de falha ocorrido; o `description` descreve o erro associado ao código de erro.
   - [`seletedProvider(mvpd)`](#$selectedProvider)

      - Disparado por `getSelectedProvider()`.
      - O `mvpd` fornece informações sobre o provedor selecionado pelo usuário.
   - [`setMetadataStatus(metadados, chave, argumentos)`](#$setMetadataStatus)

      - Disparado por `getMetadata().`
      - O `metadata` fornece os dados específicos solicitados; o `key` é a chave usada na variável `getMetadata()` pedido; e `arguments` é o mesmo dicionário passado para `getMetadata()`.
   - [&quot;preauthorizedResources(resources)`](#$preauthResources)

      - Disparado por `checkPreauthorizedResources()`.
      - O `authorizedResources` apresenta os recursos que o usuário está autorizado a visualizar.\
          










![](assets/android-entitlement-flows.png)\
 

### B. Fluxo de arranque {#startup_flow}

1. Inicie o aplicativo de nível superior.
1. Iniciar autenticação da Adobe Primetime
   1. Chame [`getInstance`](#$getInstance) para criar uma única instância do AccessEnabler de autenticação da Adobe Primetime.

      - **Dependência:** Autenticação Adobe Primetime Biblioteca nativa do Amazon FireOS (AccessEnabler)
   2. Chame` setRequestor()` Estabelecer a identificação do programador; passe no `requestorID` e (opcionalmente) uma matriz de endpoints de autenticação da Adobe Primetime.

      - **Dependência:** Autenticação Adobe Primetime válida RequestorID (Entre em contato com o Gerente de conta de autenticação da Adobe Primetime para organizar isso.)

      - **Acionadores:** retorno de chamada setRequestorComplete()

   Nenhum pedido de direito pode ser concluído até que a identidade do solicitante seja totalmente estabelecida. Isso significa efetivamente que, enquanto setRequestor() ainda estiver em execução, todas as solicitações de direito subsequentes (por exemplo,`checkAuthentication()`) estiverem bloqueadas.

   Você tem duas opções de implementação: Depois que as informações de identificação do solicitante forem enviadas para o servidor de backend, a camada do aplicativo da interface do usuário poderá escolher uma das duas abordagens a seguir:</p>

   1. Aguarde o acionamento do `setRequestorComplete()` retorno de chamada (parte do delegado AccessEnabler).  Esta opção oferece a maior certeza de que `setRequestor()` concluído, portanto, é recomendado para a maioria das implementações.

   1. Continue sem esperar o acionamento da variável `setRequestorComplete()` retorno de chamada e início da emissão de solicitações de direito. Essas chamadas (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) são enfileiradas pela biblioteca AccessEnabler, que fará as chamadas de rede reais após a `setRequestor()`. Ocasionalmente, essa opção pode ser interrompida se, por exemplo, a conexão de rede estiver instável.




1. Chame [checkAuthentication()](#$checkAuthN) para verificar uma autenticação existente sem iniciar o fluxo de Autenticação completo.  Se esta chamada for bem-sucedida, você poderá prosseguir diretamente para o fluxo de Autorização.  Caso contrário, prossiga para o fluxo Autenticação .

- **Dependência:** Uma chamada bem-sucedida para `setRequestor()` (essa dependência também se aplica a todas as chamadas subsequentes).

- **Acionadores:** retorno de chamada setAuthenticationStatus()

### C. Fluxo de autenticação {#authn_flow}

1. Chame [`getAuthentication()`](#$getAuthN) para iniciar o fluxo de autenticação ou obter confirmação de que o usuário já está autenticado. 

   **Acionadores:**  

   - O retorno de chamada setAuthenticationStatus() , se o usuário já estiver autenticado.  Nesse caso, prossiga diretamente para o [Fluxo de autorização](#authz_flow).
   - O retorno de chamada displayProviderDialog() , se o usuário ainda não estiver autenticado.  

1. Apresentar ao usuário a lista de provedores enviados para `displayProviderDialog()`.

1. Depois que o usuário selecionar um provedor, um WebView abrirá a página do provedor para que o usuário faça logon

   **Observação:** Nesse ponto, o usuário tem a oportunidade de cancelar o fluxo de autenticação. Se isso ocorrer, o AccessEnabler limpará o estado interno e redefinirá o fluxo de autenticação.

1. Após um logon bem-sucedido pelo usuário, o WebView será fechado.

1. chamada `getAuthenticationToken(),` que instrui o AccessEnabler a recuperar o token de autenticação do servidor de back-end. 

1. [Opcional] Chame [`checkPreauthorizedResources(resources)`](#$checkPreauth) para verificar quais recursos o usuário está autorizado a visualizar. O `resources` é uma matriz de recursos protegidos associada ao token de autenticação do usuário.\
   **Acionadores:** `preAuthorizedResources()` callback\
   **Ponto de execução:** Após o fluxo de autenticação concluído

1. Se a autenticação tiver sido bem-sucedida, prossiga para o Fluxo de autorização.

 

### D. Fluxo de autorização {#authz_flow}

1. Chame [`getAuthorization()`](#$getAuthZ) para iniciar o fluxo de autorização.

   Dependência: ResourceID(s) válido(s) acordado(s) com o(s) MVPD(s).

   **Observação:** ResourceIDs deve ser igual àquelas usadas em qualquer outro dispositivo ou plataforma e será o mesmo em MVPDs.

1. Validar autenticação e autorização.

   - Se a variável `getAuthorization()` chamada bem-sucedida: O usuário tem tokens AuthN e AuthZ válidos (o usuário é autenticado e autorizado a assistir a mídia solicitada).
   - If `getAuthorization()` falha: Examine a exceção lançada para determinar seu tipo (AuthN, AuthZ ou algo diferente):
      - Se foi um erro de autenticação (AuthN), reinicie o fluxo de autenticação.
      - Se foi um erro de autorização (AuthZ), o usuário não está autorizado a assistir à mídia solicitada e algum tipo de mensagem de erro deve ser exibida para o usuário.
      - Se houver algum outro tipo de erro (erro de conexão, erro de rede etc.) em seguida, exibir uma mensagem de erro apropriada para o usuário.

1. Validar o token de mídia curta.

   Use a biblioteca do Verificador de token de mídia de autenticação do Adobe Primetime para verificar o token de mídia de curta duração retornado do `getAuthorization()` acima:

   - Se a validação tiver êxito: Reproduzir a mídia solicitada para o usuário.
   - Se a validação falhar: O token AuthZ era inválido, a solicitação de mídia deve ser recusada e uma mensagem de erro deve ser exibida ao usuário.

1. Retorne ao fluxo normal do aplicativo.

### E. Visualizar fluxo de mídia {#media_flow}

1. O usuário seleciona a mídia a ser exibida.
1.  A mídia está protegida?  O aplicativo verifica se a mídia selecionada está protegida:
   - Se a mídia selecionada estiver protegida, o aplicativo iniciará o [Fluxo de autorização](#authz_flow) acima.
   - Se a mídia selecionada não estiver protegida, reproduza a mídia para o usuário.

### F. Fluxo de logout {#logout_flow}

1. Chame [`logout()`](#$logout) para fazer logoff do usuário. \
   O AccessEnabler limpa todos os valores e tokens em cache obtidos pelo usuário para o MVPD atual em todos os solicitantes que compartilham o logon por meio do Logon único. Após limpar o cache, o AccessEnabler faz uma chamada de servidor para limpar as sessões do lado do servidor.  Observe que, como a chamada do servidor pode resultar em um redirecionamento de SAML para IdP (isso permite a limpeza da sessão no lado do IdP), essa chamada deve seguir todos os redirecionamentos. Por isso, essa chamada será feita dentro de um controle WebView, invisível para o usuário.

   **Observação:** O fluxo de logout é diferente do fluxo de autenticação, pois o usuário não precisa interagir com o WebView de forma alguma. Portanto, é possível (e recomendado) tornar o controle WebView invisível (ou seja: oculto) durante o processo de logout.

