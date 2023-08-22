---
title: SDK do Amazon FireOS com registro de cliente dinâmico
description: SDK do Amazon FireOS com registro de cliente dinâmico
exl-id: 27acf3f5-8b7e-4299-b0f0-33dd6782aeda
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# SDK do Amazon FireOS com registro de cliente dinâmico {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

</br>

## <span id=""></span>Introdução {#Intro}

O SDK FireOS AccessEnabler para FireTV foi modificado para habilitar a autenticação sem usar cookies de sessão. À medida que mais e mais navegadores restringem o acesso a cookies, outro método era necessário para permitir a autenticação.

**FireOS SDK 3.0.4** substitui o mecanismo atual de registro do aplicativo com base na ID do solicitante assinada e na autenticação de cookie de sessão por [Registro de cliente dinâmico](/help/authentication/dynamic-client-registration.md).


## Alterações na API {#API}

### Factory.getInstance

**Descrição:** Instancia o objeto do Access Enabler. Deve haver uma única instância do Access Enabler por instância do aplicativo.

| Chamada de API: construtor |
| --- |
| público estático AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        gera AccessEnablerException |

**Disponibilidade:** v3.0+

**Parâmetros:**

- *appContext*: Contexto de aplicativo do Android
- *softwareStatement*: valor obtido do painel TVE ou *null* se &quot;software\_statement&quot; estiver definido em strings.xml
- *redirectUrl* : para implementações FireTV, esse parâmetro deve ser nulo. Qualquer configuração neste atributo será ignorada.

**Notas**

- software inválidoInstrução fará com que o aplicativo não inicialize o AccessEnabler ou registre o aplicativo para autenticação e autorização do Adobe Pass
- O parâmetro redirectUrl para FireTV é definido pelo SDK como adobepass://android.app, pois a autenticação é tratada por uma instância exclusiva do AccessEnabler.

### setRequestor

**Descrição:** Estabelece a identidade do Canal. Cada canal recebe um identificador exclusivo ao se registrar no Adobe para o sistema de autenticação da Adobe Primetime. Ao lidar com SSO e tokens remotos, o estado de autenticação pode mudar quando o aplicativo estiver em segundo plano, setRequestor pode ser chamado novamente quando o aplicativo for colocado em primeiro plano para sincronizar com o estado do sistema (busque um token remoto se o SSO estiver habilitado ou exclua o token local se um logout tiver ocorrido enquanto isso).

A resposta do servidor contém uma lista de MVPDs juntamente com algumas informações de configuração anexadas à identidade do Canal. A resposta do servidor é usada internamente pelo código Access Enabler. Somente o status da operação (ou seja, SUCCESS/FAIL) é apresentado ao seu aplicativo por meio do retorno de chamada setRequestorComplete().

Se a variável *urls* não for usado, a chamada de rede resultante será direcionada ao URL do provedor de serviços padrão: o ambiente de Produção da versão do Adobe.

Se um valor for fornecido para a variável *urls* parâmetro, a chamada de rede resultante será direcionada a todos os URLs fornecidos na variável *urls* parâmetro. Todas as solicitações de configuração são acionadas simultaneamente em threads separados. O primeiro respondente tem prioridade ao compilar a lista de MVPDs. Para cada MVPD na lista, o Ativador de acesso lembra o URL do provedor de serviços associado. Todas as solicitações de direito subsequentes são direcionadas ao URL associado ao provedor de serviços que foi emparelhado com o MVPD de destino durante a fase de configuração.

| Chamada de API: configuração do solicitante |
| --- |
| public void setRequestor(String requestorId) |

**Disponibilidade:** v3.0+

| Chamada de API: configuração do solicitante |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilidade:** v3.0+

**Parâmetros:**

- *requestorID*: o identificador exclusivo associado ao Canal. Transmita o identificador exclusivo atribuído pelo Adobe ao seu site quando você se registra pela primeira vez no serviço de autenticação da Adobe Primetime.
- *urls*: parâmetro opcional; por padrão, o provedor de serviços da Adobe é usado (http://sp.auth.adobe.com/). Essa matriz permite especificar endpoints para serviços de autenticação e autorização fornecidos pelo Adobe (instâncias diferentes podem ser usadas para fins de depuração). Você pode usar esta opção para especificar várias instâncias do provedor de serviços de autenticação da Adobe Primetime. Ao fazer isso, a lista MVPD é composta pelos endpoints de todos os provedores de serviços. Cada MVPD está associado ao provedor de serviços mais rápido; ou seja, o provedor que respondeu primeiro e que oferece suporte a esse MVPD.

Obsoleto:

- *signedRequestorID*: uma cópia da ID do solicitante que é assinada digitalmente com sua chave privada. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Retornos de chamada disparados:** `setRequestorComplete()`

</br>

### logout

**Descrição:** Use esse método para iniciar o fluxo de logout. O logout é o resultado de uma série de operações de redirecionamento HTTP devido ao fato de que o usuário precisa ser desconectado dos servidores de autenticação da Adobe Primetime e também dos servidores do MVPD. Como resultado, esse fluxo abrirá uma janela ChromeCustomTab para executar o logout.

| Chamada de API: iniciar o fluxo de logout |
| --- |
| public void logout() |

**Disponibilidade:** v3.0+

**Parâmetros:** Nenhum

**Retornos de chamada disparados:** `setAuthenticationStatus()`

## Fluxo de implementação do programador {#Progr}

### **1. Registrar aplicativo**

1. Obter software\_statement do Adobe Pass ( Painel TVE )
1. Há duas opções para transmitir esses valores para o SDK do Adobe Pass:
   - Em strings.xml, adicione :

     ```
     <string name>"software\_statement">[softwarestatement value]</string>
     ```

   - Chamar AccessEnabler.getInstance(appContext,softwareStatement, null)



### **2. Configurar aplicativo**

- a. setRequestor(requestor\_id)

  O SDK executará as seguintes operações:

   - registrar aplicativo: usando **software\_statement**, o SDK obterá uma **client\_id, client\_secret, client\_id\_issued\_at, redirect\_uris, grant\_types**. Essas informações serão armazenadas no armazenamento interno do aplicativo.
   - obter um **access\_token** usando client\_id, client\_secret e grant\_type=&quot;client\_credentials&quot;. Esse access\_token será usado em cada chamada feita pelo SDK para servidores da Adobe Pass.

| Respostas de Erro de Token: |  |  |
|--- | --- | --- |
| HTTP 400 (Solicitação inválida) | {&quot;error&quot;: &quot;invalid\_request&quot;} | A solicitação não tem um parâmetro obrigatório, inclui um valor de parâmetro sem suporte (diferente do tipo de concessão), repete um parâmetro, inclui várias credenciais, usa mais de um mecanismo para autenticar o cliente ou está malformada. |
| HTTP 400 (Solicitação inválida) | {&quot;error&quot;: &quot;invalid\_client&quot;} | Falha na autenticação do cliente porque o cliente era desconhecido. O SDK *DEVE* registre-se novamente no servidor de autorização. |
| HTTP 400 (Solicitação inválida) | {&quot;error&quot;: &quot;unauthorized\_client&quot;} | O cliente autenticado não está autorizado a usar este tipo de concessão de autorização. |

- no caso de um MVPD exigir Autenticação Passiva, um WebView será aberto para execução passiva com esse MVPD e será fechado quando concluído

- b. checkAuthentication()

   - *true* : ir para Autorização
   - *false* : vá para Selecionar MVPD

- c. getAuthentication : o SDK incluirá **access_token** em parâmetros de chamada

   - mvpd lembrado : ir para setSelectedProvider (mvpd\_id)
   - mvpd não selecionado : displayProviderDialog
   - mvpd selecionado : ir para setSelectedProvider(mvpd\_id)

- d. setSelectedProvider

   - O URL de autenticação mvpd\_id é carregado no ChromeCustomTabs
   - logon bem-sucedido : delegate.setAuthenticationStatus ( SUCCESS )
   - logon cancelado : redefinir seleção de MVPD
   - O esquema de URL é estabelecido como &quot;adobepass://android.app&quot; para capturar quando a autenticação é concluída

- e. get/checkAuthorization : o SDK incluirá **access\_token **in como Authorization: Bearer **access\_token**

- se a autorização for bem-sucedida, será feita uma chamada para a obtenção do token de mídia

- f. logout:

   - O SDK excluirá um token válido para o solicitante atual (as autenticações obtidas por outros aplicativos e não por meio do SSO permanecerão válidas)
   - O SDK abrirá as Guias personalizadas do Chrome para alcançar o ponto de extremidade de logout mvpd\_id. Depois de concluído, as guias personalizadas do Chrome serão fechadas
   - O esquema de URL é estabelecido como &quot;adobepass://logout&quot; para capturar o momento em que o logout é concluído
   - logout acionará um sendTrackingData(new Event(EVENT\_LOGOUT,USER\_NOT\_AUTHENTICATED\_ERROR) e um callback : setAuthenticationStatus(0,&quot;Logout&quot;)



**Nota:** já que cada chamada requer uma **access_token**, os possíveis códigos de erro abaixo são tratados no SDK.

| Respostas de erro |  |  |
|--- | --- | --- |
| invalid_request | 400 | A solicitação está malformada. O SDK deve interromper a execução de chamadas para o servidor. |
| invalid_client | 403 | A ID do cliente não tem mais permissão para executar solicitações. O sdk DEVE executar novamente o registro do cliente. |
| access_denied | 401 | O access_token não é válido. O sdk DEVE solicitar um novo access_token. |
