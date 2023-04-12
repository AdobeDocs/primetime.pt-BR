---
title: Como migrar a página de logon do MVPD do iFrame para o Pop-up
description: Como migrar a página de logon do MVPD do iFrame para o Pop-up
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Como migrar a página de logon do MVPD do iFrame para o Pop-up {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Pop-up versus iFrame {#popup-vs-iframe}

Alguns usuários encontraram problemas de cookies de terceiros com a implementação do iFrame de uma página de logon MVPD.
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

A equipe de autenticação da Adobe Primetime **A recomenda implementar a página de logon pop-up/nova janela** em vez da versão do iFrame no Firefox e Safari.  No entanto, se estiver implementando uma página de logon para o Internet Explorer, poderá encontrar problemas com a implementação de pop-up. Os problemas do IE são causados pelo fato de que, depois que o usuário se autentica com seu MVPD na janela pop-up, a autenticação do Adobe Primetime força um redirecionamento da página pai, que é visto como um bloqueador de pop-ups pelo Internet Explorer. A equipe de autenticação da Adobe Primetime **A recomenda implementar o login do iFrame para o Internet Explorer**.

O código de amostra apresentado nesta nota técnica usa uma implementação híbrida do iFrame e do popup - abrindo um iFrame no Internet Explorer e um popup em outros navegadores.

Considerando que uma implementação do iFrame já existe, a primeira parte da nota técnica apresenta o código para a implementação do iFrame e a segunda apresenta as alterações para acomodar a implementação do pop-up como padrão.


## Seletor de MVPD com página de logon em um iFrame {#mvpd-pickr-iframe}

Os exemplos de código anteriores mostravam uma página HTML que contém a variável &lt;div> adicionar uma tag onde o iFrame deve ser criado junto com o botão Fechar iFrame:

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

Aqui está o associado **JavaScript** código:

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}
```


## Seletor MVPD com página de logon em uma janela pop-up {#mvpd-pickr-popup}

Como não usaremos um **iFrame** mais, o código HTML não conterá o iFrame ou o botão para fechar o iFrame. O div que antes continha o iFrame - **mvpddiv** - serão mantidas e utilizadas para:

* para notificar o usuário que a página de logon do MVPD já está aberta caso o foco do pop-up seja perdido
* para fornecer um link para recuperar o foco no pop-up

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

A lista de MVPDs será exibida no div chamado **selecionador** como uma seleção **-mvpdList**.

Um novo retorno de chamada de API será usado - **setConfig(configXML)**. O retorno de chamada é acionado após chamar a função setRequestor(requestorID) . Esse retorno de chamada retorna a lista de MVPDs integradas ao requestorID definido anteriormente. No método de retorno de chamada, o XML de entrada será analisado e a lista de MVPDs será armazenada em cache. O seletor MVPD também é criado, mas não é exibido.

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

Depois que a função getAuthentication() ou getAuthorization() é chamada, o retorno de chamada displayProviderDialog() é acionado. Normalmente, dentro desse retorno de chamada, a lista MVPD teria sido criada e exibida. Como o seletor MVPD já foi criado, a única coisa a fazer é exibi-lo ao usuário.

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

Depois que o usuário seleciona um MVPD no seletor, o pop-up precisa ser criado. Alguns navegadores podem bloquear o pop-up se ele for criado com about:blank ou com uma página que esteja em outro domínio - portanto, é recomendável abri-lo com o nome do host de onde o AccessEnabler é carregado.

Na implementação do iFrame, a redefinição do fluxo de autenticação era feita pelo botão btnCloseIframe e pela função JavaScript closeIframeAction(), mas agora a decoração do iFrame não é mais possível. Portanto, o mesmo comportamento é obtido observando quando o pop-up é fechado (pelo usuário ou finalizando o fluxo de autenticação). Um snippet de código foi adicionado e também ajuda no caso de o usuário perder o foco do pop-up:

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

Na chamada createIFrame() , faça o retorno da função **mvpddiv** div será exibido.

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* O código de amostra contém uma variável codificada para o requestorID - &#39;REF&#39; usado, que deve ser substituído por uma ID de solicitante de programador real.
>* O código de amostra só será executado corretamente de um domínio da lista de permissões associado à ID do solicitante usada.
>* Como o código inteiro está disponível para download, o código apresentado nesta nota técnica foi truncado. Para obter uma amostra completa, consulte **iFrame JS vs Amostra de pop-up**.
>* As bibliotecas externas do JavaScript eram vinculadas do [Serviços hospedados da Google](https://developers.google.com/speed/libraries/).
