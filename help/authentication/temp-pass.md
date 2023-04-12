---
title: Passagem temporária
description: Passagem temporária
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---


# Passagem temporária {#temp-pass}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Resumo dos recursos {#tempass-featur-summary}

O Temp Pass permite que os Programadores ofereçam acesso temporário ao seu conteúdo protegido, para usuários que não têm credenciais de conta com um MVPD.  O Temp Pass inclui os seguintes recursos:

* O Temp Pass pode ser configurado para fornecer acesso temporário para cobrir uma variedade de cenários, incluindo:
   * Um programador pode oferecer uma visualização diária curta (por exemplo, de 10 minutos) de um de seus sites.
   * Um Programador pode oferecer uma apresentação única e longa (por exemplo, quatro horas) de um grande evento esportivo como as Olimpíadas ou a Marcha da NCAA Madness.
   * Um Programador pode fornecer uma combinação dos dois cenários anteriores; por exemplo, um período de visualização inicial e mais longo um dia, seguido por uma série de períodos curtos que se repetem diariamente por alguns dias subsequentes.
* Os programadores especificam a duração (Time-To-Live ou TTL) de sua passagem temporária.
* O Temp Pass opera por solicitante.  Por exemplo, a NBC pode configurar um Temp Pass de 4 horas para o solicitante &quot;NBCOlinfics&quot;.
* Os programadores podem redefinir todos os tokens concedidos a um determinado solicitante.  O &quot;MVPD temporário&quot; usado para implementar o Pass Temp deve ser configurado com &quot;Autenticação por Solicitante&quot; ativada.
* **O acesso ao Temp Pass é concedido a usuários individuais em dispositivos específicos**. Depois que o acesso à Mensagem temporária expirar para um usuário, ele não poderá obter acesso temporário no mesmo dispositivo até que o usuário tenha expirado [token de autorização](/help/authentication/glossary.md#authz-token) é apagado do servidor de autenticação da Adobe Primetime.


>[!NOTE]
>
>O Temp Pass faz parte do pacote Premium Workflow . Entre em contato com seu representante de vendas do Primetime, caso esteja interessado em usar essa funcionalidade.

## Detalhes do recurso {#tempass-featur-details}

* **Como o tempo de exibição é calculado** - A quantidade de tempo em que um Temporizador permanece válido não está correlacionada à quantidade de tempo que um usuário gasta visualizando o conteúdo no aplicativo do Programador.  Após a solicitação inicial do usuário para autorização por meio do Temp Pass, um tempo de expiração é calculado adicionando o tempo de solicitação atual inicial ao TTL especificado pelo Programador. Esse tempo de expiração está associado à ID do dispositivo do usuário e à ID do solicitante do programador e armazenado no banco de dados de autenticação do Primetime. Cada vez que o usuário tenta acessar o conteúdo usando a Mensagem temporária do mesmo dispositivo, a autenticação do Primetime comparará o tempo de solicitação do servidor com o tempo de expiração associado à ID do dispositivo do usuário e à ID do solicitante do programador. Se o tempo de solicitação do servidor for inferior ao tempo de expiração, a autorização será concedida; caso contrário, a autorização será negada.
* **Parâmetros de configuração** - Os seguintes parâmetros de passagem temporária podem ser especificados por um programador para criar uma regra de passagem temporária:
   * **TTL do token** - O tempo que um usuário tem permissão para assistir sem fazer logon em um MVPD. Essa hora é baseada em relógio e expira independentemente do usuário estar assistindo ou não conteúdo.
   >[!NOTE]
   >Uma ID de solicitante não pode ter mais de uma regra de aprovação temporária associada a ela.
* **Autenticação/Autorização** - No fluxo de aprovação de Temp, especifique o MVPD como &quot;Aprovação de Temp&quot;.  A autenticação do Primetime não se comunica com um MVPD real no fluxo de aprovação de Temp, portanto, o MVPD de &quot;Aprovação de Temp&quot; autoriza qualquer recurso. Os programadores podem especificar um recurso que pode ser acessado usando o Passe de Temp da mesma forma que fazem com o resto dos recursos em seu site. A Biblioteca do Verificador de Mídia pode ser usada como de costume para verificar o token de mídia curta de Passagem temporária e impor a verificação de recursos antes da reprodução.
* **Rastreamento de dados no fluxo de aprovação temporária** - Dois pontos em relação aos dados de rastreamento durante um fluxo de direito de passagem temporária:
   * A ID de rastreamento transmitida da autenticação do Primetime para a sua **sendTrackingData()** O retorno de chamada é um hash da ID do dispositivo.
   * Como a ID MVPD usada no fluxo de passagem Temp é &quot;Passagem Temp&quot;, essa mesma ID MVPD é passada de volta para **sendTrackingData()**. A maioria dos programadores provavelmente desejará tratar métricas de aprovação temporária de forma diferente das métricas de MVPD reais. Isso requer trabalho adicional na implementação do Analytics.

A ilustração a seguir mostra o fluxo de aprovação temporária:

![O fluxo de aprovação Temp](assets/temp-pass-flow.png)

*Figura: O fluxo de aprovação Temp*

## Implementar o Temp Pass {#implement-tempass}

No lado de autenticação do Primetime, o Temp Pass é implementado com a adição de um pseudo-MVPD chamado &quot;TempPass&quot; à configuração do servidor do Programador participante.  Este pseudo-MVPD atua como um MVPD real que concede temporariamente acesso ao conteúdo protegido do Programador.

No lado do Programador, o Temp Pass é implementado da seguinte maneira para os dois cenários que os MVPDs usam para autenticação:

* **iFrame na página do programador**. O Temp Pass funciona independentemente do tipo de autenticação de MVPD, mas para o cenário do iFrame são necessárias etapas adicionais para cancelar o fluxo de autenticação atual e autenticar com o Temp Pass. Essas etapas são mostradas na seção [Logon do iFrame](/help/authentication/temp-pass.md) abaixo.
* **Redirecionar para página de logon do MVPD**. No caso mais tradicional em que a interface do usuário para acionar a aprovação temporária é apresentada antes de iniciar a autenticação com um MVPD, não há etapas especiais a serem tomadas. O Temp Pass deve ser tratado como um MVPD regular.

Os pontos a seguir se aplicam a ambos os cenários de implementação:

* O &quot;Temp Pass&quot; deve ser exibido no seletor de MVPD somente para usuários que ainda não solicitaram uma autorização de Temp Pass. Bloquear a exibição de solicitações subsequentes pode ser feito mantendo um sinalizador em cookies. Isso funcionará desde que o usuário não limpe o cache do navegador. Se os usuários limparem os caches do navegador, o &quot;Temporizador&quot; será exibido novamente no seletor e o usuário poderá solicitá-lo novamente. O acesso será concedido somente se o tempo &quot;Teste temporário&quot; ainda não tiver expirado.
* Quando um usuário solicita acesso por meio do Pass Temp, o Servidor de autenticação Primetime não executará a solicitação SAML (Security Assertion Markup Language) normal durante o processo de autenticação. Em vez disso, o ponto de extremidade de autenticação retornará o sucesso sempre que for chamado enquanto os tokens forem válidos para o dispositivo.
* Quando um Temp Pass expira, seu usuário não será mais autenticado, pois no Fluxo de aprovação temporária o token de autenticação e o token de autorização têm a mesma data de expiração. Para explicar aos usuários que seu Temp Pass expirou, os Programadores devem recuperar o MVPD selecionado logo após chamar `setRequestor()`e, em seguida, chame `checkAuthentication()` como de costume. No `setAuthenticationStatus()` retorno de chamada uma verificação pode ser feita para determinar se o status de autenticação é 0, de modo que, se o MVPD selecionado foi &quot;TempPass&quot;, uma mensagem pode ser apresentada aos usuários que sua sessão de aprovação temporária expirou.
* Se um usuário excluir o token de aprovação temporária antes da expiração, as verificações de direito subsequentes gerarão um token que terá um TTL igual ao tempo restante.
* Se o usuário excluir o token de aprovação temporária após a expiração, as verificações de direito subsequentes retornarão &quot;usuário não autorizado&quot;.

Veja as amostras em [Código de exemplo](/help/authentication/temp-pass.md#tempass-sample-code) abaixo para obter exemplos de como codificar os detalhes de implementação descritos nesta seção.

## Código de exemplo {#tempass-sample-code}

As seções abaixo mostram como chamar a API de autenticação do Primetime para implementar o fluxo de passagem temporária:

* [Exemplo de login do iFrame](/help/authentication/temp-pass.md#iframe-login-sample)
* [Amostra de logon automático](/help/authentication/temp-pass.md#auto-login-sample)

### Exemplo de login do iFrame {#iframe-login-sample}

Este exemplo mostra como implementar o Temp Pass para o caso em que os MVPDs oferecem suporte à integração do iFrame:

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>
```

#### Casos de uso do logon do iFrame {#iframe-login-use-cases}

**Para solicitar um Temp Pass pela primeira vez:**

1. Um usuário acessa a página do Programador e clica no link de logon.
1. O seletor MVPD é aberto e o usuário escolhe um MVPD da lista.
1. O iFrame de autenticação é exibido. Este iFrame contém um link &quot;Temp Pass&quot;.
1. O usuário clica em &quot;Passe de Temp&quot;, de modo que o Programador adiciona um sinalizador a um cookie para impedir que o usuário veja o link &quot;Passe de Temp&quot; em visitas subsequentes à página.
1. A solicitação de autenticação Temp Pass chega aos servidores de autenticação Primetime e gera um token de autenticação. O TTL é igual ao período definido pelo Programador para a passagem temporária.
1. A solicitação de autorização de Aprovação Temp chega aos servidores de autenticação Primetime.
1. Os servidores de autenticação do Primetime extraem as IDs do dispositivo e do solicitante da solicitação e as armazenam no banco de dados junto com o tempo de expiração. O tempo de expiração é calculado como: tempo de solicitação de aprovação temporária inicial mais o TTL (especificado pelo programador).
1. Os servidores de autenticação do Primetime geram um token de autorização.
1. O usuário acessa o conteúdo protegido.

**Para solicitar um Relatório temporário novamente depois que um usuário recorrente do Relatório temporário tiver excluído os cookies do navegador:**

1. O usuário acessa a página do Programador e clica no link de logon.
1. O seletor MVPD é aberto e o usuário escolhe um MVPD da lista.
1. O iFrame de autenticação é exibido. Este iFrame contém um link &quot;Temp Pass&quot; (o usuário excluiu o cookie original, de modo que o Programador não sabe se o usuário clicou no link &quot;Temp Pass&quot; antes).
1. O usuário clica novamente em &quot;Teste temporário&quot;, de forma que o Programador adicione um sinalizador a um cookie novamente, para impedir que o usuário veja o link &quot;Passagem temporária&quot; em visitas subsequentes à página.
1. A solicitação de autenticação Temp Pass chega aos servidores de autenticação Primetime, que geram um token de autenticação. O TTL agora é o tempo restante para a aprovação temporária (a diferença entre a hora atual e o tempo de expiração associado à ID do dispositivo).
1. A solicitação de autorização de Aprovação Temp chega aos servidores de autenticação Primetime.
1. Os servidores de autenticação do Primetime extraem as IDs do dispositivo e do solicitante da solicitação e as usam para recuperar o tempo de expiração do banco de dados de autenticação do Primetime. A hora atual é comparada à hora de expiração.
1. Se o Temp Pass do usuário não tiver expirado, os servidores de autenticação do Primetime gerarão um token de autorização.
1. Se o Temp Pass do usuário não tiver expirado, ele poderá acessar o conteúdo protegido.

### Amostra de logon automático {#auto-login-sample}

A amostra a seguir ilustra um caso em que um usuário é conectado automaticamente com o TempPass ao visitar um site. O usuário pode optar por fazer logon com um MVPD regular a qualquer momento e é avisado se o TempPass expirou:

```HTML
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## Utilizar múltiplas estações Temp {#use-mult-tempass}

Alguns eventos exigem acesso gratuito em fases ao conteúdo, como um intervalo inicial de acesso livre (por exemplo, 4 horas), seguido de acessos gratuitos diários (por exemplo, 10 minutos em cada dia subsequente).  Para que um Programador implemente este cenário, ele deve organizá-lo com seu Adobe para configurar dois MVPDs temporários para o Programador.

Para este cenário de exemplo (uma sessão inicial livre de 4 horas, seguida por sessões diárias gratuitas de 10 minutos), o Adobe configura um MVPD chamado TempPass1 com um Time-To-Live (TTL) de 4 horas e um TempPass2 com um TTL de 10 minutos para o período subsequente.  Ambos estão associados à ID do solicitante do programador.

### Implementação do programa {#mult-tempass-prog-impl}

Depois que o Adobe configurar as duas instâncias TempPass, os dois MVPDs adicionais (TempPass1 e TempPass2) aparecerão na lista MVPD do Programador.  O Programador precisa seguir as etapas a seguir para implementar as várias etapas temporárias:

1. Na visita inicial do usuário ao site, faça logon automaticamente com TempPass1. Você pode usar a Amostra de Logon Automática acima como um ponto de partida para esta tarefa.
1. Ao detectar que o TempPass1 expirou, armazene o fato (em um cookie/armazenamento local) e apresente ao usuário seu seletor MVPD padrão. **Certifique-se de filtrar TempPass1 e TempPass2 dessa lista**.
1. Em cada dia subsequente, se TempPass1 tiver expirado, faça o logon automático desse usuário com TempPass2.
1. Quando TempPass2 expirar, armazene o fato (em um cookie/armazenamento local) do dia e apresente ao usuário seu seletor MVPD padrão. Novamente, certifique-se de filtrar TempPass1 e TempPass2 dessa lista.
1. Em cada novo dia, às 00:00 horas, redefina todas as passagens temporárias para TempPass2, usando o [Redefinir API Web TempPass](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**Nota de programação:** A Autenticação do Primetime não tem um mecanismo integrado para interromper o streaming gratuito após os 10 minutos terem passado.  Cabe aos programadores restringir o acesso assim que o TempPass2 expirar. Para conseguir isso, os Programadores podem implementar em seus sites/aplicativos uma chamada &quot;checkAuthorization&quot; a cada X minutos, onde X é o período que o Programador determina que faz sentido para seus aplicativos.

## Redefinir todas as aprovações de Temp {#reset-all-tempass}

Determinadas regras comerciais exigem a limpeza regular do Temp Pass ou uma redefinição ad hoc de todas as Mensagens Temp emitidas para uma ID de Solicitante e ID MVPD específica. Esse recurso suporta casos de uso como os seguintes:

* Um Temp Pass diário de 10 minutos (o Temp Pass deve ser redefinido no início do dia)
* Um Temp Pass disponível para todos os usuários durante as últimas notícias. (O Temp Pass precisa ser redefinido para todos os dispositivos assim que as notícias de última hora começarem.)
* O cenário de Vencimento múltiplo temporário que fornece uma combinação de um período de visualização inicial de algum comprimento, seguido de períodos diários subsequentes de outro tamanho.

Para redefinir todos os Temp Pass, a autenticação do Primetime fornece aos Programadores uma *público* API da Web:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>O URL acima substitui a API de redefinição anterior. A antiga API de redefinição (v1) não é mais suportada.

* **Protocolo:** HTTPS
* **Host:**
   * Versão - mgmt.auth.adobe.com
   * Prequal - mgmt-prequal.auth.adobe.com
* **Caminho:** /reset-tempass/v2/reset
* **Parâmetros de consulta:** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **Cabeçalhos:** ApiKey - 1232293681726481
* **Resposta:**
   * Sucesso - HTTP 204
   * Falha:
      * HTTP 400 para uma solicitação incorreta
      * HTTP 401 se a ApiKey não tiver sido especificada
      * HTTP 403 se a ApiKey for inválida

Por exemplo:

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## Clientes compatíveis {#supp-clients}

Suporte à ferramenta Temp Pass and Reset por plataforma:

| Clientes de autenticação da Adobe Primetime | Aprovação temporária | Ferramenta Redefinir |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | SIM | SIM |
| iOS cliente nativo | SIM | SIM |
| TvOS do cliente nativo | SIM | SIM |
| Android de cliente nativo | SIM | SIM |
| FireTV de cliente nativo | SIM | SIM |
| API sem cliente | SIM | SIM |

## Limitações e problemas conhecidos {#limitations}

Esta seção descreve as limitações que se aplicam à implementação atual do Temp Pass.

**SDK do JavaScript**: suporta a funcionalidade de redefinição de aprovação temporária da versão **3.X e superior**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->