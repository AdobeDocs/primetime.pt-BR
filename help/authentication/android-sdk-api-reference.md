---
title: Referência da API do SDK do Android
description: Referência da API do SDK do Android
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4517'
ht-degree: 0%

---



# Referência da API do SDK do Android {#android-sdk-api-reference}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#intro}

Este documento detalha os métodos e retornos de chamada expostos pelo Android SDK para autenticação da Adobe Primetime, com suporte nas versões de autenticação da Adobe Primetime 1.7 e posteriores. Os métodos e as funções de retorno de chamada descritos aqui são definidos nos arquivos de cabeçalho AccessEnabler.h e EntitlementDelegate.h .

Consulte [https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library) para obter o SDK do Android AccessEnabler mais recente. 


**Observação:** A equipe de autenticação da Adobe Primetime incentiva o uso somente da autenticação da Adobe Primetime *público* APIs:

- As APIs públicas estão disponíveis *e totalmente testadas* em todos os tipos de clientes suportados. Para qualquer recurso público, garantimos que cada tipo de cliente tenha uma versão correspondente do(s) método(s) associado(s).</span>
- As APIs públicas devem ser o mais estáveis possível, para oferecer suporte à compatibilidade com versões anteriores e garantir que as integrações de parceiros não sejam interrompidas. No entanto, para *non*-APIs públicas, reservamos o direito de alterar sua assinatura em qualquer ponto futuro. Se você encontrar um fluxo específico que não pode ser suportado por meio de uma combinação das chamadas de API de autenticação públicas atuais do Adobe Primetime, a melhor abordagem é nos informar. Levando em conta suas necessidades, podemos modificar as APIs públicas e fornecer uma solução estável a partir de agora.

## API do Android {#api}

- [getInstance](#getInstance)
- [setOptions](#setOptions)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSeletedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- pré-autorizar
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [logout](#logout)
- [getSeletedProvider](#getSelectedProvider)
- [seletedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

### Factory.getInstance {#getInstance}

**Descrição:** Instancia o objeto Access Enabler. Deve haver uma única instância do Access Enabler por instância de aplicativo.

| Chamada da API: construtor |
| --- |
| **estática pública** AccessEnabler **getInstance**(Context appContext, String softwareStatement, String redirectUrl)<br>        **garras** AccessEnablerException <br><br>**estática pública** AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl)<br>**garras** AccessEnablerException |

**Disponibilidade:** v3.1.2+

**Parâmetros:**

- *appContext*: Contexto do aplicativo Android.
- env\_url: para testar usando o ambiente de preparo do Adobe, env\_url pode ser definido como &quot;sp.auth-staging.adobe.com&quot;

**Obsoleto:**

```
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```



### setRequestor {#setRequestor}

**Descrição:** Estabelece a identidade do Programador. Cada Programador recebe uma ID exclusiva ao se registrar no Adobe para o sistema de autenticação da Adobe Primetime. Ao lidar com o SSO e tokens remotos, o estado de autenticação pode mudar quando o aplicativo está em segundo plano, setRequestor pode ser chamado novamente quando o aplicativo é trazido para o primeiro plano para sincronizar com o estado do sistema (busque um token remoto se o SSO estiver ativado ou exclua o token local se um logout tiver ocorrido enquanto isso).

A resposta do servidor contém uma lista de MVPDs junto com algumas informações de configuração anexadas à identidade do Programador. A resposta do servidor é usada internamente pelo código Access Enabler . Somente o status da operação (ou seja, SUCCESS/FAIL) é apresentado ao seu aplicativo por meio do retorno de chamada setRequestorComplete() .

Se a variável *urls* não for usado, a chamada de rede resultante será direcionada ao URL padrão do provedor de serviços: o ambiente de liberação/produção do Adobe.

Se um valor for fornecido para a variável *urls* , a chamada de rede resultante é direcionada a todos os URLs fornecidos no *urls* parâmetro. Todas as solicitações de configuração são acionadas simultaneamente em threads separados. O primeiro entrevistado tem precedência ao compilar a lista de MVPDs. Para cada MVPD na lista, o Criador de Acesso lembra o URL do provedor de serviços associado. Todas as solicitações de direito subsequentes são direcionadas para o URL associado ao provedor de serviços que foi emparelhado com o MVPD de destino durante a fase de configuração.

| Chamada da API: configuração do solicitante |
| --- |
| ```public void setRequestor(String requestorId)``` |

**Disponibilidade:** v3.0+

| Chamada da API: configuração do solicitante |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |
**Disponibilidade:** v3.0+


**Parâmetros:**

- *requestorID*: A ID exclusiva associada ao Programador. Passe a ID exclusiva atribuída pelo Adobe ao seu site quando se registrou pela primeira vez no serviço de autenticação da Adobe Primetime.

- *signedRequestorID*: Uma cópia da ID do solicitante que é assinada digitalmente com sua chave privada. <!--For more details. see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

- *urls*: Parâmetro opcional; por padrão, o provedor de serviços da Adobe é usado (http://sp.auth.adobe.com/). Essa matriz permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (diferentes instâncias podem ser usadas para fins de depuração). Você pode usar isso para especificar várias instâncias do provedor de serviços de autenticação da Adobe Primetime. Ao fazer isso, a lista MVPD é composta pelos pontos de extremidade de todos os provedores de serviços. Cada MVPD está associado ao prestador de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que suporta esse MVPD.

**Retornos de chamada acionados:** `setRequestorComplete()`

Obsoleto:

    public void setRequestor(String requestorId, String signedRequestorId)
    
    public void setRequestor (String requestorId, String signedRequestorId, ArrayList&lt;string> urls)

[Voltar para a API do Android...](#api)

### setRequestorComplete {#setRequestorComplete}

**Descrição:** Retorno de chamada acionado pelo Ativador de acesso que informa ao aplicativo que a fase de configuração está concluída. Este é um sinal de que o aplicativo pode iniciar a emissão de solicitações de direito. Nenhum pedido de direito pode ser emitido pelo aplicativo até a fase de configuração ser concluída.

| Retorno de chamada: configuração do solicitante concluída |
| --- |
| público java void setRequestorComplete(int status) |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *status*: Pode assumir um dos seguintes valores:
   - SDK \>= 3.4.0
      - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS` - a fase de configuração foi concluída com êxito
      - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR` - falha na fase de configuração
   - SDK \&lt; 3.4
      - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - a fase de configuração foi concluída com êxito
      - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - falha na fase de configuração

**Disparado por:** `setRequestor()`

[Voltar para a API do Android...](#api)

### setOptions {#setOptions}

**Descrição:** Define opções globais do SDK. Aceita um **Mapa\&lt;string string=&quot;&quot;>** como um argumento. Os valores do mapa serão passados para o servidor juntamente com todas as chamadas de rede feitas pelo SDK.

Os valores serão transmitidos ao servidor independentemente do fluxo atual (autenticação/autorização). Se quiser alterar os valores, você pode chamar esse método em qualquer momento.

| Chamada da API: setOptions |
| --- |
| public void setOptions(HashMap)&lt;string string=&quot;&quot;> options) |

**Disponibilidade:** v1.9.2+

**Parâmetros:**

- *opções*: Um mapa&lt;string string=&quot;&quot;> contendo opções globais do SDK. Atualmente, as seguintes opções estão disponíveis:
   - **applicationProfile** - Ele pode ser usado para fazer configurações de servidor com base nesse valor.
   - **ap_vi** - A visitorID do Marketing Cloud. Esse valor pode ser usado posteriormente em relatórios de análise avançados.
   - **ap_ai** - A ID de publicidade
   - **device_info** - Informações do cliente, conforme descrito aqui: [Enviando a conexão e o aplicativo do dispositivo de informações do cliente](/help/authentication/passing-client-information-device-connection-and-application.md).

[Voltar ao topo...](#apis)


### checkAuthentication {#checkAuthN}

**Descrição:** Verifica o status de autenticação. Ele faz isso procurando por um token de autenticação válido no espaço de armazenamento de token local. Chamar esse método não executa chamadas de rede. Ele é usado pelo aplicativo para consultar o status de autenticação do usuário e atualizar a interface do usuário adequadamente (ou seja, atualizar a interface de logon / logout). O status de autenticação é comunicado ao aplicativo por meio da variável [*setAuthenticationStatus()*](#setAuthNStatus) retorno de chamada.

Se um MVPD suportar o recurso &quot;Autenticação por Solicitante&quot;, vários tokens de autenticação poderão ser armazenados em um dispositivo.  Para obter detalhes sobre este recurso, consulte o [Diretrizes de armazenamento em cache](#$caching) na seção Visão geral técnica do Android.

| Chamada da API: verificar status de autenticação |
| --- |
| public void checkAuthentication() |

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** `setAuthenticationStatus()`

[Voltar para a API do Android...](#api)


### getAuthentication {#getAuthN}

**Descrição:** Inicia o fluxo de trabalho de autenticação completo. Ele é iniciado verificando o status de autenticação. Se ainda não estiver autenticado, a máquina de estado do fluxo de autenticação será iniciada:

- Se a última tentativa de autenticação foi bem-sucedida, a fase de seleção do MVPD é ignorada e a variável [*navigateToUrl()*](#navigagteToUrl) o retorno de chamada é acionado. O aplicativo usa essa chamada de retorno para instanciar o controle WebView que apresenta ao usuário a página de logon do MVPD.
- Se a última tentativa de autenticação não tiver sido bem-sucedida ou se o usuário tiver feito logout explicitamente, a variável [*displayProviderDialog()*](#displayProviderDialog) o retorno de chamada é acionado. Seu aplicativo usa esse retorno de chamada para exibir a interface de seleção do MVPD. Além disso, seu aplicativo é necessário para retomar o fluxo de autenticação, informando a biblioteca do Ativador de Acesso sobre a seleção do MVPD do usuário por meio do [setSeletedProvider()](#setSelectedProvider) método .

À medida que as credenciais do usuário são verificadas na página de logon do MVPD, seu aplicativo é necessário para monitorar as várias operações de redirecionamento que ocorrem enquanto o usuário é autenticado na página de logon do MVPD. Quando as credenciais corretas são inseridas, o controle WebView é redirecionado para um URL personalizado definido pela variável *AccessEnabler.ADOBEPASS\_REDIRECT\_URL* constante. Esse URL não deve ser carregado pelo WebView. O aplicativo deve interceptar esse URL e interpretar esse evento como um sinal de que a fase de logon está concluída. Em seguida, ele deve entregar o controle ao Ativador de acesso para concluir o fluxo de autenticação (chamando o *getAuthenticationToken()* método ).

Se um MVPD suportar o recurso &quot;Autenticação por Solicitante&quot;, vários tokens de autenticação poderão ser armazenados em um dispositivo (um por Programador).  Para obter detalhes sobre este recurso, consulte o [Diretrizes de armazenamento em cache](#$caching) na seção Visão geral técnica do Android.

Por fim, o status de autenticação é comunicado ao aplicativo por meio da variável *setAuthenticationStatus()* retorno de chamada.



| Chamada da API: inicia o fluxo de autenticação |
| --- |
| public void getAuthentication() |

**Disponibilidade:** v1.0+

| Chamada da API: inicia o fluxo de autenticação |
| --- |
| public void getAuthentication(boolean forceAuthN, Map&lt;string object=&quot;&quot;> genericData) |

**Disponibilidade:** v1.8+

**Parâmetros:**

- *forceAuthn*: Um sinalizador que especifica se o fluxo de autenticação deve ser iniciado, independentemente de o usuário já estar autenticado ou não.
- *dados*: Um mapa que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK.

**Retornos de chamada acionados:** `setAuthenticationStatus(), displayProviderDialog(), navigateToUrl(), sendTrackingData()`


[Voltar para a API do Android...](#api)

### displayProviderDialog {#displayProviderDialog}

**Descrição** O retorno de chamada acionado pelo Ativador de acesso para informar ao aplicativo que os elementos apropriados da interface do usuário precisam ser instanciados para permitir que o usuário selecione o MVPD desejado. O retorno de chamada fornece uma lista de objetos MVPD com informações adicionais que podem ajudar a criar corretamente o painel da interface de seleção (como o URL apontando para o logotipo do MVPD, nome de exibição amigável etc.)

Depois que o usuário seleciona o MVPD desejado, o aplicativo da camada superior é necessário para retomar o fluxo de autenticação chamando *setSeletedProvider()* e transmitindo a ID do MVPD correspondente à seleção do usuário.\
 
>[!NOTE]
>
> Abortar o fluxo de autenticação
> </br></br>
> Observe que esse é um ponto em que o usuário tem a capacidade de pressionar o botão &quot;Voltar&quot;, o que equivale à interrupção do fluxo de autenticação. Nesse cenário, o aplicativo é obrigado a chamar a função `setSelectedProvider()` método , passando *null* como parâmetro, para dar ao Ativador de Acesso a oportunidade de redefinir sua máquina de estado de autenticação.

| Retorno de chamada: exibir a interface de seleção do MVPD |
| --- |
| `public void displayProviderDialog(ArrayList<Mvpd> mvpds)` |

**Disponibilidade:** v1.0+

**Parâmetros**:

- *mvpds*: Lista de objetos MVPD que contêm informações relacionadas ao MVPD que o aplicativo pode usar para criar os elementos da UI de seleção do MVPD.

**Disparado por:** `getAuthentication(), getAuthorization()`

[Voltar para a API do Android...](#api)


### setSeletedProvider {#setSelectedProvider}

**Descrição:** Este método é chamado pelo seu aplicativo para informar o Ativador de Acesso sobre a seleção MVPD do usuário. O aplicativo pode usar esse método para selecionar ou alterar o provedor de serviços usado para autenticação.

Se o MVPD selecionado for um MVPD TempPass, ele será autenticado automaticamente com esse MVPD sem precisar chamar getAuthentication() depois.

Observe que isso não é possível para o Pass de Temp Promocional, onde parâmetros extras são fornecidos no método getAuthentication() .

Ao passar *null* como parâmetro, o Access Enabler assume que o usuário cancelou o fluxo de autenticação (ou seja, pressionou o botão &quot;Voltar&quot;) e responde redefinindo a máquina de estado de autenticação e chamando a função *setAuthenticationStatus()* retorno de chamada com o `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR` código de erro.

| Chamada da API: definir o provedor selecionado no momento |
| --- |
| public void setSeletedProvider(String mvpdId) |

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** `setAuthenticationStatus(), sendTrackingData(), navigateToUrl()`

[Voltar para a API do Android...](#api)


### navigateToUrl {#navigagteToUrl}

**Obsoleto:** A partir do Android SDK 3.0, o navigateToUrl é usado somente se a guia Personalizada do Chrome não estiver presente no dispositivo

**Descrição:** Retorno de chamada acionado pelo Ativador de Acesso que informa ao aplicativo que o usuário precisa ser apresentado com a página de logon MVPD para inserir suas credenciais. O Ativador de Acesso transmite como parâmetro o URL da página de logon do MVPD. Seu aplicativo é necessário para instanciar um controle WebView e direcioná-lo para esse URL. Além disso, o aplicativo é necessário para monitorar os URLs carregados pelo controle WebView e interceptar a operação de redirecionamento direcionando o URL personalizado definido pelo `AccessEnabler.ADOBEPASS_REDIRECT_URL (deprecated)` constante. Nesse evento, o aplicativo é obrigado a fechar ou ocultar o controle do WebView e fornecer o controle de volta à biblioteca do Ativador de Acesso, chamando o *getAuthenticationToken()* método . O Ativador de Acesso conclui o fluxo de autenticação recuperando o token de autenticação do servidor de back-end e armazenando-o localmente no armazenamento do token.  

>[!WARNING]
>
> **Abortar o fluxo de autenticação**  <br>Observe que esse é um ponto em que o usuário tem a capacidade de pressionar o botão &quot;Voltar&quot;, o que equivale à interrupção do fluxo de autenticação. Nesse cenário, o aplicativo é obrigado a chamar a função _setSeletedProvider()_ aprovação de método _null_ como o parâmetro e dando uma chance ao Enabler de acesso para redefinir sua máquina de estado de autenticação.

| Retorno de chamada: exibir página de logon MVPD |
| --- |
| public void navigateToUrl(String url) |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *url*: O URL que aponta para a página de logon do MVPD

**Disparado por:** `getAuthentication(), setSelectedProvider()`

[Voltar para a API do Android...](#api)


### getAuthenticationToken {#getAuthNToken}

**Obsoleto:** A partir do Android SDK 3.0, como a guia Personalizado do Chrome é usada para autenticação, esse método não é mais usado do aplicativo.

**Descrição:** Conclui o fluxo de autenticação solicitando o token de autenticação do servidor de back-end. Este método deve ser chamado pelo seu aplicativo somente em resposta a um evento em que o controle WebView que hospeda a página de logon MVPD é redirecionado para o URL personalizado definido pelo `AccessEnabler.ADOBEPASS_REDIRECT_URL` constante.

| Chamada da API: recuperar o token de autenticação |
| --- |
| public void getAuthenticationToken() |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *cookies*: Cookies definidos no domínio de destino (consulte o aplicativo de demonstração no SDK para obter uma implementação de referência).

**Retornos de chamada acionados:** `setAuthenticationStatus()`, `sendTrackingData()`

[Voltar para a API do Android...](#api)


### setAuthenticationStatus {#setAuthNStatus}

**Descrição:** Retorno de chamada acionado pelo Ativador de acesso que informa o aplicativo sobre o status do fluxo de autenticação. Há muitos locais em que esse fluxo pode falhar, seja como resultado da interação do usuário ou devido a outros cenários imprevistos (ou seja, problemas de conectividade de rede etc.). Esse retorno de chamada informa o aplicativo sobre o status de sucesso/falha do fluxo de autenticação, fornecendo também informações adicionais sobre o motivo da falha, quando necessário.

| Retorno de chamada: relatar o status do fluxo de autenticação |
| --- |
| public void setAuthenticationStatus(int status, String errorCode) |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *status*: Pode assumir um dos seguintes valores:
   - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS` - o fluxo de autenticação foi concluído com êxito
   - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR` - falha no fluxo de autenticação
- *código*: Motivo da falha. If *status* é `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`, em seguida *código* é uma string vazia (ou seja, definida pela variável `AccessEnablerConstants.USER_AUTHENTICATED` constante). Em caso de falha, esse parâmetro pode assumir um dos seguintes valores:
   - `AccessEnablerConstants.USER_NOT_AUTHENTICATED_ERROR` - O usuário não está autenticado. Em resposta à *checkAuthentication()* chamada de método quando não houver um token de autenticação válido no cache de token local.
   - `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR` - O AccessEnabler redefiniu a máquina de estado de autenticação após a aprovação do aplicativo de camada superior *null* para `setSelectedProvider()` para suspender o fluxo de autenticação.  Provavelmente, o usuário cancelou o fluxo de autenticação (ou seja, pressionou o botão &quot;Voltar&quot;).
   - `AccessEnablerConstants.GENERIC_AUTHENTICATION_ERROR` - O fluxo de autenticação falhou devido a motivos como indisponibilidade da rede ou o usuário cancelou explicitamente o fluxo de autenticação.

**Disparado por:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

[Voltar para a API do Android...](#api)


### checkPreauthorizedResources {#checkPreauth}

>**Obsoleto:** A partir do Android SDK 3.6, a API de pré-autorização está substituindo checkPreauthorizedResources, fornecendo códigos de erro estendidos. 

**Descrição:** Esse método é usado pelo aplicativo para determinar se o usuário já está autorizado a visualizar recursos protegidos específicos. O objetivo principal desse método é recuperar informações para uso na decoração da interface do usuário (por exemplo, indicando o status de acesso com ícones de bloqueio e desbloqueio).

| Chamada da API: definir o provedor selecionado no momento |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**Disponibilidade:** v1.3+

**Parâmetros:** O `resources` é uma matriz de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID do recurso está sujeita às mesmas limitações que a ID do recurso na `getAuthorization()` ou seja, deve ser um valor acordado estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia.

**Retorno de chamada acionado:** `preauthorizedResources()`

[Voltar para a API do Android...](#api)


### checkPreauthorizedResources {#checkPreauth2}

**Obsoleto:** A partir do Android SDK 3.6, a API de pré-autorização está substituindo checkPreauthorizedResources, fornecendo códigos de erro estendidos. 

**Descrição:** Esse método é usado pelo aplicativo para determinar se o usuário já está autorizado a visualizar recursos protegidos específicos. O objetivo principal desse método é recuperar informações para uso na decoração da interface do usuário (por exemplo, indicando o status de acesso com ícones de bloqueio e desbloqueio).

| Chamada da API: definir o provedor selecionado no momento |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources, boolean cache)` |

**Disponibilidade:** v3.1+

**Parâmetros:** O `resources` é uma matriz de recursos para os quais a autorização deve ser verificada. Cada elemento na lista deve ser uma string que representa a ID do recurso. A ID do recurso está sujeita às mesmas limitações que a ID do recurso na `getAuthorization()` ou seja, deve ser um valor acordado estabelecido entre o Programador e o MVPD ou um fragmento RSS de mídia.

O `cache` especifica se a resposta de pré-autorização em cache pode ser usada ou não. Por padrão, o cache é verdadeiro, o SDK retornará uma resposta armazenada em cache anteriormente, se disponível.

**Retorno de chamada acionado:** `preauthorizedResources()`

[Voltar para a API do Android...](#api)

### preauthorizedResources {#preauthResources}

**Obsoleto:** A partir do Android SDK 3.6, a API de pré-autorização está substituindo checkPreauthorizedResources, fornecendo códigos de erro estendidos. o retorno de chamada preauthorizedResources não será chamado na nova API.


**Descrição:** Retorno de chamada acionado por checkPreauthorizedResources(). Fornece uma lista de recursos que o usuário já está autorizado a visualizar.

| Chamada da API: definir o provedor selecionado no momento |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**Disponibilidade:** v1.3+

**Parâmetros:** O `resources` é uma matriz de recursos para os quais o usuário já está autorizado a visualizar.

**Disparado por:** `checkPreauthorizedResources()`

[Voltar para a API do Android...](#api)

### <span id="checkAuthZ"></span>checkAuthorization

**Descrição:** Este método é usado pelo aplicativo para verificar o status da autorização. Ele é iniciado verificando primeiro o status de autenticação. Se não estiver autenticado, a variável *setTokenRequestFailed()* o retorno de chamada é acionado e o método sai. Se o usuário estiver autenticado, ele também acionará o fluxo de autorização. Veja os detalhes da *getAuthorization()* método .

| Chamada da API: verificar status de autorização |
| --- |
| public void checkAuthorization(String resourceId) |

**Disponibilidade:** v1.0+

| Chamada da API: verificar status de autorização |
| --- |
| public void checkAuthorization(String resourceId, Mapa&lt;string object=&quot;&quot;> genericData) |

**Disponibilidade:** v1.8+

**Parâmetros:**

- *resourceId*: A ID do recurso para o qual o usuário solicita autorização.
- *dados*: Um mapa que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK.

**Retornos de chamada acionados:** `tokenRequestFailed(), setToken(),sendTrackingData(), setAuthenticationStatus()`

[Voltar para a API do Android...](#api)


### <span id="getAuthZ"></span>getAuthorization

**Descrição:** Este método é utilizado pelo pedido para iniciar o fluxo de autorização. Se o usuário ainda não estiver autenticado, ele também iniciará o fluxo de autenticação. Se o usuário for autenticado, o Ativador de Acesso continuará a emitir solicitações para o token de autorização (se nenhum token de autorização válido estiver presente no cache de token local) e para o token de mídia de curta duração. Quando o token de mídia curto for obtido, o fluxo de autorização será considerado concluído. O *setToken()* o retorno de chamada é acionado e o token de mídia curto é entregue como parâmetro para o aplicativo. Se, por qualquer motivo, a autorização falhar, a variável *tokenRequestFailed()* a chamada de retorno é acionada e o código de erro e os detalhes são fornecidos.

| Chamada da API: iniciar o fluxo de autorização |
| --- |
| public void getAuthorization(String resourceId) |

**Disponibilidade:** v1.0+

| Chamada da API: iniciar o fluxo de autorização |
| --- |
| public void getAuthorization(String resourceId, Mapa&lt;string object=&quot;&quot;> genericData) |

**Disponibilidade:** v1.8+

**Parâmetros:**

- *resourceId*: A ID do recurso para o qual o usuário solicita autorização.
- *dados*: Um mapa que consiste em pares de valores chave a serem enviados para o serviço de passagem de TV paga. O Adobe pode usar esses dados para ativar a funcionalidade futura sem alterar o SDK. 

**Retornos de chamada acionados:** `tokenRequestFailed(), setToken(), sendTrackingData()`

>[!WARNING]
>
> **Retornos de chamada adicionais acionados**  <br> Esse método também pode acionar os seguintes retornos de chamada (se o fluxo de autenticação também for iniciado): *setAuthenticationStatus()*, *displayProviderDialog()*, *navigateToUrl()*

**OBSERVAÇÃO: Use checkAuthorization() em vez de getAuthorization() sempre que possível. O método getAuthorization() iniciará um fluxo de autenticação completo (se o usuário não estiver autenticado) e isso pode levar a uma implementação complicada no lado do Programador.**

[Voltar para a API do Android...](#api)


### setToken {#setToken}

**Descrição:** Retorno de chamada acionado pelo Ativador de Acesso que informa ao seu aplicativo que o fluxo de autorização foi concluído com êxito. O token de mídia de curta duração também é fornecido como parâmetro.

| Retorno de chamada: fluxo de autorização concluído com êxito |
| --- |
| public void setToken(String token, String resourceId) |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *token*: O token de mídia de curta duração
- *resourceId*: O recurso para o qual a autorização foi obtida

**Disparado por:** `checkAuthorization()`, `getAuthorization()`


[Voltar para a API do Android...](#api)

### tokenRequestFailed {#tokenRequestFailed}

**Descrição:** Retorno de chamada acionado pelo Ativador de acesso que informa ao aplicativo da camada superior que o fluxo de autorização falhou.

| Retorno de chamada: falha no fluxo de autorização |
| --- |
| public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription) |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *resourceId*: O recurso para o qual a autorização foi obtida
- *errorCode*: Código de erro associado ao cenário de falha. Valores possíveis:
   - `AccessEnablerConstants.USER_NOT_AUTHORIZED_ERROR` - O usuário não pôde autorizar o recurso em questão
- *errorDescription*: Detalhes adicionais sobre o cenário de falha. Se essa string descritiva não estiver disponível por qualquer motivo, a autenticação da Adobe Primetime envia uma string vazia **(&quot;&quot;)**.

   Essa sequência de caracteres pode ser usada por um MVPD para passar mensagens de erro personalizadas ou mensagens relacionadas a vendas. Por exemplo, se uma autorização para um recurso for negada a um assinante, o MVPD poderá enviar uma mensagem como: &quot;No momento, você não tem acesso a esse canal no seu pacote. Se quiser atualizar seu pacote, clique aqui.&quot; A mensagem é passada pela autenticação da Adobe Primetime por meio dessa chamada de retorno para o Programador, que tem a opção de exibi-la ou ignorá-la. A autenticação da Adobe Primetime também pode usar esse parâmetro para fornecer uma notificação da condição que pode ter levado a um erro. Por exemplo, &quot;Ocorreu um erro de rede ao comunicar com o serviço de autorização do fornecedor&quot;.

**Disparado por:** `checkAuthorization(), getAuthorization()`

[Voltar para a API do Android...](#api)

### logout {#logout}

**Descrição:** Use esse método para iniciar o fluxo de logout. O logout é o resultado de uma série de operações de redirecionamento HTTP devido ao fato de que o usuário precisa ser desconectado dos servidores de autenticação da Adobe Primetime e também dos servidores MVPD. Como resultado, esse fluxo não pode ser concluído com uma simples solicitação HTTP emitida pela biblioteca do Access Enabler. Uma guia Personalizada do Chrome é usada pelo SDK para executar as operações de redirecionamento HTTP. Esse fluxo será visível para o usuário e fechado quando concluído

| Chamada da API: iniciar o fluxo de logout |
| --- |
| public void logout() |

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:**

- `navigateToUrl()` para a versão do SDK anterior à 3.0
- `setAuthenticationStatus()` para SDK versão > 3.0


[Voltar para a API do Android...](#api)


### getSeletedProvider {#getSelectedProvider}

**Descrição:** Use este método para determinar o provedor selecionado no momento.

| Chamada da API: determinar o MVPD atualmente selecionado |
| --- |
| public void getSeletedProvider() |

**Disponibilidade:** v1.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** `selectedProvider()`

[Voltar para a API do Android...](#api)


### <span id="selectedProvider"></span>seletedProvider

**Descrição:** Retorno de chamada acionado pelo Ativador de Acesso que fornece informações sobre o MVPD atualmente selecionado para o aplicativo.

| Retorno de chamada: informações sobre o MVPD atualmente selecionado |
| --- |
| public void seletedProvider(Mvpd mvpd) |


**Disponibilidade:** v1.0+

**Parâmetros:**

- *mvpd*: Objeto que contém informações sobre o MVPD atualmente selecionado

**Disparado por:** `getSelectedProvider()`

[Voltar para a API do Android...](#api)


### getMetadata {#getMetadata}

**Descrição:** Use esse método para recuperar informações expostas como metadados pela biblioteca do Ativador de acesso. O aplicativo pode acessar essas informações fornecendo um objeto MetadataKey composto.

| Chamada da API: consultar os metadados do AccessEnabler |
| --- |
| `public void getMetadata(MetadataKey metadataKey)` |

**Disponibilidade:** v1.0+

Há dois tipos de metadados disponíveis para Programadores:

- Metadados estáticos (TTL do token de autenticação, TTL do token de autorização e ID do dispositivo) 
- Metadados do usuário (informações específicas do usuário, como ID de usuário e CEP; passadas de um MVPD para o dispositivo de um usuário durante os fluxos de Autenticação e/ou Autorização)

**Parâmetros:**

- *metadataKey*: Uma estrutura de dados que encapsula uma variável de chave e args, com o seguinte significado:
   - Se a chave for `METADATA_KEY_USER_META` e args contém um objeto SerializableNameValuePair com name = `METADATA_ARG_USER_META` e valor = `[metadata_name]`, em seguida, o query é feito para metadados do usuário. A lista atual de tipos de metadados de usuário disponíveis:
      - `zip` - CEP

      - `householdID` - Identificador da família. Se um MVPD não suportar subcontas, isso será idêntico ao `userID`.

      - `maxRating` - Classificação parental máxima para o usuário

      - `userID` - O identificador do usuário. Se um MVPD suportar subcontas e o usuário não for a conta principal, `userID` será diferente de `householdID`.

      - `channelID` - Uma lista de canais que o usuário tem direito a visualizar
   - Se a chave for `METADATA_KEY_DEVICE_ID` em seguida, o query é feito para obter a id do dispositivo atual. Observe que esse recurso está desativado por padrão e os programadores devem entrar em contato com o Adobe para obter informações sobre ativação e tarifas.
   - Se a chave for `METADATA_KEY_TTL_AUTHZ` e args contém um objeto SerializableNameValuePair com name = `METADATA_ARG_RESOURCE_ID` e valor = `[resource_id]`, o query é feito para obter o tempo de expiração do token de autorização associado ao recurso especificado.
   - Se a chave for `METADATA_KEY_TTL_AUTHN` em seguida, o query é feito para obter o tempo de expiração do token de autenticação. 

 

>[!NOTE]
>
>Para o SDK 3.4.0, as constantes : `METADATA_KEY_USER_META, METADATA_KEY_DEVICE_ID, METADATA_KEY_TTL_AUTHZ, METADATA_KEY_TTL_AUTHN` estão disponíveis em com.adobe.adobepass.access.enabler.api.profile.UserProfileService.



>[!NOTE]
>
>Os metadados de usuário reais disponíveis para um Programador dependem do que um MVPD disponibiliza.  Essa lista será expandida ainda mais à medida que novos metadados forem disponibilizados e adicionados ao sistema de autenticação da Adobe Primetime.

**Retornos de chamada acionados:** [`setMetadataStatus()`](#setMetadaStatus)

**Mais informações:** [Metadados do usuário](/help/authentication/user-metadata-feature.md)

[Voltar para a API do Android...](#api)

### setMetadataStatus {#setMetadaStatus}

**Descrição:** Retorno de chamada acionado pelo Ativador de acesso que fornece os metadados solicitados por meio de um *getMetadata()* chame.

| Retorno de chamada: resultado da solicitação de recuperação de metadados |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *key*: O objeto MetadataKey que contém a chave para a qual o valor de metadados é solicitado e os parâmetros associados (consulte o aplicativo de demonstração para obter uma implementação de referência).
- *resultado*: Um objeto composto contendo os metadados solicitados. O objeto tem os seguintes campos:
   - *simpleResult*: uma String que representa o valor dos metadados quando a solicitação foi feita para TTL de autenticação, TTL de autorização ou ID do dispositivo. Esse valor é nulo se a solicitação foi feita para Metadados do usuário.

   - *userMetadataResult*: um Objeto que contém a representação Java de uma carga de metadados do usuário JSON.\
      Por exemplo:

```json
          '{
          "street": "Main Avenue",
          "buildings": ["150", "320"]
          }'
```

é traduzido para Java como: 

```java
          Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
```

**A estrutura real dos objetos de metadados do usuário é semelhante ao seguinte:**

```json
          {
              updated: 1334243471,
              encrypted: ["encryptedProp"],
              data: {
                  zip: ["12345", "34567"],
                  maxRating: { 
                      "MPAA": "PG-13",
                      "VCHIP": "TV-Y", 
                      "URL": "http://exam.pl/e/manage/ratings"
                  },
                  householdID: "3456",
                  userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                  channelID: ["channel-1", "channel-2"]
              }
          }
```

Esse valor é nulo quando a solicitação foi feita para metadados simples (TTL de autenticação, TTL de autorização ou ID do dispositivo).

- *criptografado*: Valor booleano que especifica se os metadados recuperados são criptografados ou não. Esse parâmetro é importante somente para solicitações de Metadados do usuário, não tem significado para Metadados estáticos (por exemplo: TTL de autenticação) que é sempre recebida sem criptografia. Se este parâmetro for definido como Verdadeiro, cabe ao Programador obter o valor de Metadados de Usuário Não criptografados executando uma descriptografia RSA usando a chave privada da lista de permissões (a mesma chave privada usada para a assinatura da ID do solicitante no [`setRequestor`](#setRequestor) call).

**Disparado por:** [`getMetadata()`](#getMetadata)

**Mais informações:** [Metadados do usuário](/help/authentication/user-metadata-feature.md)


[Voltar para a API do Android...](#api)


### getVersion {#getVersion}

**Descrição:** Este método pode ser usado para recuperar a versão da biblioteca AccessEnabler .

| Chamada da API: obter a versão do AccessEnabler |
| --- |
| ```public static String getVersion()``` |


[Voltar para a API do Android...](#api)

</br>

## Rastreamento de eventos {#tracking}

O Ativador de acesso aciona um retorno de chamada adicional que não está necessariamente relacionado aos fluxos de direito. Implementar a função de retorno de chamada de rastreamento de eventos chamada *sendTrackingData()* é opcional, mas permite que o aplicativo rastreie eventos específicos e compile estatísticas, como o número de tentativas de autenticação/autorização bem-sucedidas/com falha. Abaixo está a especificação do *sendTrackingData()* retorno de chamada:\
 

### sendTrackingData {#sendTrackingData}

**Descrição:** Retorno de chamada acionado pelo Ativador de Acesso que sinaliza para o aplicativo a ocorrência de vários eventos, como a conclusão/falha dos fluxos de autenticação/autorização. O tipo de dispositivo, o tipo de cliente Access Enabler e o sistema operacional também são relatados por sendTrackingData().

>[!WARNING]
>
> O tipo de dispositivo e o sistema operacional são derivados por meio do uso de uma biblioteca Java pública ([http://java.net/projects/user-agent-utils](http://java.net/projects/user-agent-utils)) e a sequência do agente do usuário. Esteja ciente de que essas informações são fornecidas apenas como uma maneira abrangente de detalhar métricas operacionais em categorias de dispositivos, mas o Adobe não pode se responsabilizar por resultados incorretos. Use a nova funcionalidade adequadamente.


- Valores possíveis para o tipo de dispositivo:
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`


- Valores possíveis para o tipo de cliente Access Enabler:
   - `flash`
   - `html5`
   - `ios`
   - `android`

</br>

| Retorno de chamada: rastreamento de eventos |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**Disponibilidade:** v1.0+

**Parâmetros:**

- *evento*: o evento que está sendo rastreado. Há três tipos possíveis de eventos de rastreamento:
   - **authorizationDetection:** sempre que uma solicitação de token de autorização retornar (o tipo de evento é `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection:** sempre que ocorrer uma verificação de autenticação (o tipo de evento é `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** quando o usuário seleciona um MVPD no formulário de seleção MVPD (o tipo de evento é `EVENT_MVPD_SELECTION`)
- *dados*: dados adicionais associados ao evento reportado. Esses dados são apresentados no formato de uma lista de valores.

A seguir estão instruções para interpretar os valores no *dados*
array:

- Para tipo de evento *`EVENT_AUTHN_DETECTION`:*
   - **0** - Se a solicitação de token foi bem-sucedida (true/false) e se o acima é verdadeiro:
   - **1** - Cadeia de caracteres de ID de MVPD
   - **2** - GUID (hash md5)
   - **3** - Token já em cache (true/false)
   - **4** - Tipo de dispositivo
   - **5** - Tipo de cliente Access Enabler
   - **6** - Tipo de sistema operacional

- Para tipo de evento `EVENT_AUTHZ_DETECTION`
   - **0** - Se a solicitação de token foi bem-sucedida (true/false) e se foi bem-sucedida:
   - **1** - ID MVPD
   - **2** - GUID (hash md5)
   - **3** - Token já em cache (true/false)
   - **4** - Erro
   - **5** - Detalhes
   - **6** - Tipo de dispositivo
   - **7** - Tipo de cliente Access Enabler
   - **8** - Tipo de sistema operacional

- Para tipo de evento `EVENT_MVPD_SELECTION`
   - **0** - ID do MVPD atualmente selecionado
   - **1** - Tipo de dispositivo
   - **2** - Tipo de cliente Access Enabler
   - **3** - Tipo de sistema operacional

**Disparado por:** `checkAuthentication()`, `getAuthentication()`, `checkAuthorization()`, `getAuthorization()`, `setSelectedProvider()`

[Voltar para a API do Android...](#api)


<!--
## Related Information {#related}

- [Android Integration Cookbook](/help/authentication/android-sdk-cookbook.md)
- [Android Technical Overview](/help/authentication/android-sdk-overview.md)

-->
