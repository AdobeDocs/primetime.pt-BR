---
title: Amazon FireOS SDK com Registro dinâmico de clientes
description: Amazon FireOS SDK com Registro dinâmico de clientes
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---


# Amazon FireOS SDK com Registro dinâmico de clientes {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## <span id=""></span>Introdução {#Intro}

O FireOS AccessEnabler SDK para FireTV foi modificado para habilitar a Autenticação sem usar cookies de sessão. À medida que mais e mais navegadores restringem o acesso aos cookies, outro método era necessário para permitir a autenticação.

**FireOS SDK 3.0.4** substitui o mecanismo de registro do aplicativo atual com base na ID de solicitante assinada e na autenticação de cookie de sessão por [Registro dinâmico de clientes](/help/authentication/dynamic-client-registration.md).
 

## Alterações na API {#API}

### Factory.getInstance

**Descrição:** Instancia o objeto Access Enabler. Deve haver uma única instância do Access Enabler por instância de aplicativo.

| Chamada da API: construtor |
| --- |
| public static AccessEnabler getInstance (Context appContext, String softwareStatement, String redirectUrl)<br>        lança AccessEnablerException |

**Disponibilidade:** v3.0+

**Parâmetros:**

- *appContext*: Contexto do aplicativo Android
- *softwareStatement*: valor obtido do painel TVE ou *null* se &quot;software\_statement&quot; estiver definido em strings.xml
- *redirectUrl* : para implementações FireTV, esse parâmetro deve ser nulo. Quaisquer configurações neste atributo serão ignoradas. 

**Notas**

- softwareStatement inválido fará com que o aplicativo não inicialize o AccessEnabler ou registre o aplicativo para autenticação e autorização Adobe Pass
- O parâmetro redirectUrl para FireTV é definido pelo SDK para adobepass://android.app as a autenticação é realizada pela instância exclusiva AccessEnabler.

### setRequestor

**Descrição:** Estabelece a identidade do Canal. Cada Canal recebe uma ID exclusiva ao se registrar no Adobe para o sistema de autenticação da Adobe Primetime. Ao lidar com o SSO e tokens remotos, o estado de autenticação pode mudar quando o aplicativo está em segundo plano, setRequestor pode ser chamado novamente quando o aplicativo é trazido para o primeiro plano para sincronizar com o estado do sistema (busque um token remoto se o SSO estiver ativado ou exclua o token local se um logout tiver ocorrido enquanto isso).

A resposta do servidor contém uma lista de MVPDs junto com algumas informações de configuração anexadas à identidade do Canal. A resposta do servidor é usada internamente pelo código Access Enabler . Somente o status da operação (ou seja, SUCCESS/FAIL) é apresentado ao seu aplicativo por meio do retorno de chamada setRequestorComplete() .

Se a variável *urls* não for usado, a chamada de rede resultante será direcionada ao URL padrão do provedor de serviços: o ambiente Adobe Release Production .

Se um valor for fornecido para a variável *urls* , a chamada de rede resultante é direcionada a todos os URLs fornecidos no *urls* parâmetro. Todas as solicitações de configuração são acionadas simultaneamente em threads separados. O primeiro entrevistado tem precedência ao compilar a lista de MVPDs. Para cada MVPD na lista, o Criador de Acesso lembra o URL do provedor de serviços associado. Todas as solicitações de direito subsequentes são direcionadas para o URL associado ao provedor de serviços que foi emparelhado com o MVPD de destino durante a fase de configuração.

| Chamada da API: configuração do solicitante |
| --- |
| public void setRequestor(String requestorId) |

**Disponibilidade:** v3.0+

| Chamada da API: configuração do solicitante |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilidade:** v3.0+

**Parâmetros:**

- *requestorID*: A ID exclusiva associada ao Canal. Passe a ID exclusiva atribuída pelo Adobe ao seu site ao se registrar pela primeira vez no serviço de autenticação da Adobe Primetime.
- *urls*: Parâmetro opcional; por padrão, o provedor de serviços da Adobe é usado (http://sp.auth.adobe.com/). Essa matriz permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (diferentes instâncias podem ser usadas para fins de depuração). Você pode usar isso para especificar várias instâncias do provedor de serviços de autenticação da Adobe Primetime. Ao fazer isso, a lista MVPD é composta pelos pontos de extremidade de todos os provedores de serviços. Cada MVPD está associado ao prestador de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que suporta esse MVPD.

Obsoleto:

- *signedRequestorID*: Uma cópia da ID do solicitante que é assinada digitalmente com sua chave privada. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Retornos de chamada acionados:** `setRequestorComplete()`

</br>

### logout

**Descrição:** Use esse método para iniciar o fluxo de logout. O logout é o resultado de uma série de operações de redirecionamento HTTP devido ao fato de que o usuário precisa ser desconectado dos servidores de autenticação da Adobe Primetime e também dos servidores MVPD. Como resultado, esse fluxo abrirá uma janela ChromeCustomTab para executar o logout.

| Chamada da API: iniciar o fluxo de logout |
| --- |
| public void logout() |

**Disponibilidade:** v3.0+

**Parâmetros:** Nenhum

**Retornos de chamada acionados:** `setAuthenticationStatus()`

## Fluxo de implementação do programa {#Progr}

### **1. Registrar aplicativo** 

1. Obter software\_statement da Adobe Pass ( Painel TVE )
1. Há duas opções para transmitir esses valores para o Adobe Pass SDK :
   - Em strings.xml , adicione : 

      ```
      <string name>"software\_statement">[softwarestatement value]</string>
      ```

   - Chame AccessEnabler.getInstance(appContext,softwareStatement, null)

 

### **2. Configurar aplicativo**

- a.  setRequestor(requestor\_id) 

   O SDK executará as seguintes operações: 

   - pedido de registro: usar **software\_statement**, o SDK obterá um **client\_id, client\_secret, client\_id\_issued\_at, redirect\_uris, grant\_types**. Essas informações serão armazenadas no armazenamento interno do aplicativo.
   - obter um **access\_token** usando client\_id, client\_secret e grant\_type=&quot;client\_credentials&quot; . Esse acesso\_token será usado em cada chamada feita pelo SDK para os servidores da Adobe Pass.

| Respostas de erro de token : |  |  |
|--- | --- | --- |
| HTTP 400 (Solicitação inválida) | {&quot;erro&quot;: &quot;invalid\_request&quot;} | Falta um parâmetro obrigatório na solicitação, inclui um valor de parâmetro não suportado (diferente do tipo concessão), repete um parâmetro, inclui várias credenciais, utiliza mais de um mecanismo para autenticar o cliente ou está malformado. |
| HTTP 400 (Solicitação inválida) | {&quot;erro&quot;: &quot;invalid\_client&quot;} | Falha na autenticação do cliente porque o cliente era desconhecido. O SDK *DEVE* registre-se novamente no servidor de autorização. |
| HTTP 400 (Solicitação inválida) | {&quot;erro&quot;: &quot;unauthorized\_client&quot;} | O cliente autenticado não está autorizado a usar este tipo de concessão de autorização. |

- caso um MVPD exija Autenticação Passiva, um WebView será aberto para executar passivo com esse MVPD e será fechado quando concluído

- b. checkAuthentication()

   - *true* : ir para Autorização
   - *false* : ir para Selecionar MVPD

- c. getAuthentication : o SDK incluirá **access_token** em parâmetros de chamada 

   - mvpd lembrado : vá para setSeletedProvider(mvpd\_id)
   - mvpd não selecionado : displayProviderDialog
   - mvpd selecionado : vá para setSeletedProvider(mvpd\_id)

- d. setSeletedProvider

   - O url de autenticação mvpd\_id é carregado no ChromeCustomTabs
   - logon bem-sucedido : delegate.setAuthenticationStatus ( SUCCESS )
   - logon cancelado : redefinir seleção MVPD
   - O esquema de URL é estabelecido como &quot;adobepass://android.app&quot; para capturar quando a autenticação for concluída

- e. get/checkAuthorization : O SDK incluirá **access\_token **no cabeçalho como Autorização: Portador **access\_token**

- se a autorização for bem-sucedida, será feita uma chamada para obter o token de mídia

- f. logout : 

   - O SDK excluirá o token válido para o solicitante atual (as autenticações obtidas por outros aplicativos e não por meio do SSO permanecerão válidas)
   - O SDK abrirá as Guias personalizadas do Chrome para acessar o endpoint de logout mvpd\_id . Uma vez concluídas, as guias personalizadas do Chrome serão fechadas
   - O esquema de URL é estabelecido como &quot;adobepass://logout&quot; para capturar o momento em que o logout é concluído
   - logout acionará um sendTrackingData(new Event(EVENT\_LOGOUT,USER\_NOT\_AUTHENTICATED\_ERROR) e um retorno de chamada : setAuthenticationStatus(0,&quot;Logout&quot;)

 

**Observação:** como cada chamada requer uma **access_token**, possíveis códigos de erro abaixo são manipulados no SDK. 

| Respostas de erro |  |  |
|--- | --- | --- |
| invalid_request | 400 | A solicitação está malformada. O SDK deve parar de executar chamadas para o servidor. |
| invalid_client | 403 | A ID do cliente não tem mais permissão para executar solicitações. O sdk DEVE executar novamente o registro do cliente. |
| access_denied | 401 | O access_token não é válido. O sdk DEVE solicitar um novo access_token. |

