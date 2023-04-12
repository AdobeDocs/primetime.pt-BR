---
title: Logon e Logout sem Atualização
description: Logon e Logout sem Atualização
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---


# Logon e Logout sem Atualização {#tefresh-less-login-and-logout}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Para aplicativos da Web, você deve considerar alguns cenários possíveis diferentes para autenticar e desconectar usuários.  Os MVPDs exigem que os usuários façam logon na página da Web do MVPD para se autenticarem, com os seguintes fatores adicionais a serem reproduzidos:

- Alguns MVPDs exigem um redirecionamento completo do site para a página de logon
- Alguns MVPDs exigem que você abra um iFrame em seu site para exibir a página de logon do MVPD
- Alguns navegadores não lidam bem com o cenário do iFrame, portanto, para esses navegadores, uma alternativa melhor é usar uma janela pop-up em vez do iFrame

Antes da autenticação 2.7 da Adobe Primetime, todos esses cenários para a autenticação de um usuário envolviam uma atualização de página completa da página do Programador. Para as versões 2.7 e subsequentes, a equipe de autenticação da Adobe Primetime melhorou esses fluxos para que o usuário não tenha que experimentar uma atualização de página no seu aplicativo durante o logon e o logout.  


## Descrição detalhada {#detailed_description}

Vamos começar com um resumo dos fluxos de autenticação e logout originais e seguir com os fluxos de autenticação e logout aprimorados. Observe que as primeiras quatro seções abordam MVPDs normais (não TempPass), enquanto a última seção descreve a implementação especial que precisa ser aplicada para TempPass:

- [Fluxo de autenticação original](#orig_authn)
- [Fluxo de logout original](#orig_logout)
- [Fluxo de autenticação aprimorado](#improved_authn)
- [Fluxo de logout aprimorado](#improved_logout)
- [Fluxo TempPass](#improved_temppass)

</br>

## Autenticação Original / Fluxos de Logout {#orig_authn}

**Autenticação**

Os clientes da Web de autenticação da Adobe Primetime têm duas maneiras de autenticação, dependendo dos requisitos dos MVPDs:

1. **Redirecionamento de página inteira -** Depois que o usuário seleciona um provedor (configurado com redirecionamento de página inteira) do seletor de MVPD no site do Programador, `setSelectedProvider(<mvpd>)` é chamado no AccessEnabler e o usuário é redirecionado para a página de logon do MVPD. Depois que o usuário fornecer credenciais válidas, ele será redirecionado de volta ao site do Programador. O AccessEnabler é inicializado e o token de autenticação é recuperado da autenticação da Adobe Primetime durante `setRequestor`.
1. **iFrame / Janela Pop-up -** Depois que o usuário seleciona um provedor (configurado com iFrame), `setSelectedProvider(<mvpd>)` é chamado no AccessEnabler. Essa ação acionará a `createIFrame(width, height)` retorno de chamada, notificando o Programador para criar um iFrame (ou pop-up - dependendo do navegador/preferências) com o nome `"mvpdframe"` e as dimensões fornecidas. Depois que o iFrame/pop-up é criado, o AccessEnabler carrega a página de logon do MVPD no iFrame/pop-up. O usuário fornece credenciais válidas e o iFrame/popup é redirecionado para a autenticação da Adobe Primetime, que retorna um trecho JS que fecha o iFrame/popup e recarrega a página pai (site do Programador). De maneira semelhante ao fluxo 1, o token de autenticação é recuperado durante `setRequestor`. 

O `displayProviderDialog` retorno de chamada (acionado por `getAuthentication`/`getAuthorization`) retorna uma lista de MVPDs e suas configurações apropriadas. O `iFrameRequired` A propriedade de um MVPD permite que o Programador saiba se ele deve ativar o fluxo 1 ou o fluxo 2. Observe que o Programador deve realizar ações extras (criação de um iFrame/pop-up) somente para o fluxo 2.

**Cancelar autenticação**

Há também a situação em que o usuário cancela explicitamente o fluxo de autenticação fechando a página de logon. Aqui estão os cenários e a solução proposta para os programadores:

1. **Redirecionamento de página inteira -** Quando a página de logon for fechada, o usuário precisará navegar novamente para o site do Programador e iniciar todo o fluxo desde o início. Não é necessária nenhuma ação explícita do lado do Programador neste cenário.
1. **iFrame -** Recomenda-se que o Programador hospede o iFrame dentro de um `div` (ou componente de interface de usuário semelhante) que tem um botão Fechar anexado a ele. Quando o usuário pressiona o botão Fechar, o Programador destruirá o iFrame junto com a interface do usuário associada e executará `setSelectedProvider(null)`. Essa chamada permite que o AccessEnabler limpe seu estado interno e possibilite que o usuário inicie um fluxo de autenticação subsequente. `setAuthenticationStatus` e `sendTrackingData(AUTHENTICATION_DETECTION...)` será acionado para sinalizar um fluxo de autenticação com falha (ambos ativados `getAuthentication` e `getAuthorization`).
1. **Pop-up -** Alguns navegadores não conseguem detectar com precisão o evento de fechamento da janela, portanto, é necessário adotar uma abordagem diferente aqui (em contraste com o fluxo do iFrame acima). O Adobe recomenda que o Programador inicialize um temporizador que verifique periodicamente a existência do pop-up de logon. Se a janela não existir, o Programador pode ter certeza de que o usuário cancelou manualmente o fluxo de login e o Programador pode continuar com a chamada `setSelectedProvider(null)`. Os retornos de chamada acionados são os mesmos do fluxo 2 acima.

</br>

## Fluxo de logout original {#orig_logout}

A API de logout do AccessEnabler limpa o estado local da biblioteca e carrega o URL de logout do MVPD na guia/janela atual. O navegador navega até o terminal de logout do MVPD e, após a conclusão do processo, o usuário é redirecionado de volta ao site do Programador. A única ação necessária em nome do usuário é pressionar o botão/link Logout e iniciar o fluxo; nenhuma interação do usuário é necessária no terminal de logout do MVPD.

**Fluxo de autenticação/logout original com atualização de página**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## Autenticação aprimorada (sem atualização) {#improved_authn}

>[!NOTE]
>
>Os fluxos aprimorados de logon e logout sem atualização exigem que o navegador ofereça suporte às modernas tecnologias HTML5, incluindo mensagens da Web.

Os fluxos de autenticação (logon) e de logout discutidos acima fornecem uma experiência do usuário semelhante ao recarregar a página principal após a conclusão de cada fluxo.  O recurso atual visa melhorar a experiência do usuário fornecendo logon e logout sem atualização (em segundo plano). O Programador pode ativar/desativar o logon e o logout em segundo plano passando dois sinalizadores booleanos (`backgroundLogin` e `backgroundLogout`) à `configInfo` do `setRequestor` API. Por padrão, o logon/logout em segundo plano é desativado (isso oferece compatibilidade com a implementação anterior).

**Exemplo:**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**Autenticação**

Os pontos a seguir descrevem a transição entre os fluxos de autenticação originais e os fluxos aprimorados:

1. O redirecionamento de página inteira é substituído por uma nova guia do navegador na qual o logon do MVPD é executado. O Programador é necessário para criar uma nova guia (via `window.open`) nomeado `mvpdwindow` quando o usuário seleciona um MVPD (com `iFrameRequired = false`). O Programador é executado `setSelectedProvider(<mvpd>)`, permitindo que o AccessEnabler carregue o URL de logon do MVPD na nova guia. Depois que o usuário fornecer credenciais válidas, a autenticação da Adobe Primetime fechará a guia e enviará window.postMessage para o site do Programador que sinaliza para o AccessEnabler que o fluxo de autenticação foi concluído. Os seguintes retornos de chamada são acionados:

   - Se o fluxo tiver sido iniciado por `getAuthentication`: `setAuthenticationStatus` e `sendTrackingData(AUTHENTICATION_DETECTION...)` será acionado para sinalizar autenticação bem-sucedida/malsucedida.

   - Se o fluxo tiver sido iniciado por `getAuthorization`: `setToken/tokenRequestFailed` e `sendTrackingData(AUTHORIZATION_DETECTION...)` será acionado para sinalizar a autorização bem-sucedida/mal-sucedida.

1. O fluxo da janela do iFrame / pop-up permanece praticamente inalterado, com a diferença de que, depois que o usuário fornece credenciais válidas, a página pai não será recarregada. O iFrame/pop-up será fechado automaticamente após o logon e um `window.postMessage` é enviada para a página principal, notificando o AccessEnabler de que o fluxo foi concluído. Os mesmos retornos de chamada são acionados como no fluxo anterior, **além do novo retorno de chamada a seguir: `destroyIFrame`**. O `destroyIFrame` O retorno de chamada permite que o Programador remova qualquer componente associado/auxiliar do iFrame, como decorações da interface do usuário. A existência desse retorno de chamada não era necessária no fluxo de autenticação antigo porque, após a conclusão do logon, a autenticação da Adobe Primetime recarregaria a página do Programador, destruindo todos os componentes da interface do usuário.

</br>     

>[!IMPORTANT]
> 
>Você deve carregar o iFrame de login ou a janela pop-up do MVPD como um filho direto da página que contém a instância AccessEnabler. Se o iFrame de login ou a janela pop-up do MVPD estiver aninhado em dois ou mais níveis abaixo da página que contém a instância AccessEnabler, o fluxo poderá travar. Por exemplo, se você tivesse um iFrame localizado entre a página principal e o iFrame MVPD (Página =\> iFrame =\> iFrame MVPD), o fluxo de logon poderia falhar.

</br>

 **Cancelar autenticação**

Esses são os fluxos para cancelar a autenticação:

1. **Guia Navegador -** Como a guia é basicamente uma nova janela, a captura de seu evento close tem as mesmas limitações que foram discutidas no cenário 3 dos fluxos de autenticação antigos. Além disso, a abordagem do temporizador não é possível aqui, porque não há como distinguir uma guia que foi fechada manualmente pelo usuário de uma guia que foi fechada automaticamente no fim do fluxo de logon. A solução aqui é que o AccessEnabler permaneça &quot;silencioso&quot; (nenhum retorno de chamada é acionado) quando o usuário cancela o fluxo. Além disso, o Programador não é obrigado a tomar nenhuma ação específica. O usuário poderá iniciar outro fluxo de autenticação sem receber o erro &quot;Erro de várias solicitações de autenticação&quot; (esse erro foi desativado no AccessEnabler para logon em segundo plano).

1. **iFrame -** O Programador pode adotar a abordagem discutida no cenário 2 a partir dos fluxos de autenticação antigos (crie a interface do usuário do wrapper a partir do iFrame e o botão Fechar associado que é acionado `setSelectedProvider(null)`. Embora essa abordagem não seja mais um requisito sólido (vários fluxos de autenticação são permitidos para logon em segundo plano, como discutido no cenário 1 acima), ela ainda é recomendada pelo Adobe.

1. **Pop-up -** Isso é idêntico ao fluxo da guia Navegador acima.

</br>

## Fluxo de logout aprimorado {#improved_logout}

O novo fluxo de logout será executado em um iFrame oculto, eliminando o redirecionamento da página inteira.  Isso é possível porque o usuário não precisa tomar uma ação específica na página de logout do MVPD.

Após concluir o fluxo de logout, ele redirecionará o iFrame para um endpoint de autenticação personalizado da Adobe Primetime. Isso servirá um trecho de JS que executa uma `window.postMessage` ao pai, notificando ao AccessEnabler que o logout foi concluído. Os seguintes retornos de chamada são acionados: `setAuthenticationStatus()` e `sendTrackingData(AUTHENTICATION_DETECTION ...)`, sinalizando que o usuário não está mais autenticado. 

A ilustração abaixo mostra o fluxo sem atualização que permite ao usuário fazer logon no MVPD sem atualizar a página principal do aplicativo:

**Autenticação/Fluxo de logout aprimorado (sem atualização)**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## Fluxo TempPass {#improved_temppas}

O logon sem atualização segue uma abordagem diferente para MVPDs do tipo TempPass.

Como o fluxo TempPass requer que uma janela seja criada automaticamente e fechada sem interação explícita com o usuário, isso pode causar problemas para alguns navegadores (bloqueadores de pop-up). Portanto, o AccessEnabler implementa a fase de logon nos bastidores, sem exigir um contêiner da Web criado pelo Programador.

Estes são os aspectos que o Programador precisa conhecer ao implementar o TempPass para logon e logout sem atualização:

- Antes de iniciar a autenticação, a janela do iFrame ou pop-up precisa ser criada somente para MVPDs que não sejam TempPass. O Programador pode detectar se um MVPD é TempPass ou não lendo o `tempPass` propriedade do objeto MVPD (retornado por `setConfig()` / `displayProviderDialog()`).

- O `createIFrame()` O retorno de chamada deve conter uma verificação para TempPass e executar sua lógica somente quando o MVPD NÃO for TempPass.

- O `destroyIFrame()` O retorno de chamada deve conter uma verificação para TempPass e executar sua lógica somente quando o MVPD NÃO for TempPass.

- O `setAuthenticationStatus()` e `sendTrackingData()` os retornos de chamada são disparados após a conclusão da autenticação (exatamente como no fluxo sem atualização para MVPDs normais).

>[!NOTE]
>
>Esse fluxo está disponível somente para TempPass sem Atualização. Para o fluxo de atualização, TempPass precisa ser manipulado explicitamente (quando TempPass requer iFrame / popup)

</br>

A amostra de código a seguir demonstra como lidar com uma janela MVPD em um site do Programador (tanto para MVPDs normais quanto para TempPass):

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```

