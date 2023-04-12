---
title: Guia de migração do iOS/tvOS v3.x
description: Guia de migração do iOS/tvOS v3.x
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Guia de migração do iOS/tvOS v3.x {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

>[!TIP]
> 
> **Notas:**
>
> - A partir do iOS sdk versão 3.1, os implementadores agora podem usar WKWebView ou UIWebView alternadamente. Como UIWebView está obsoleta, os aplicativos devem migrar para WKWebView, para evitar problemas com versões futuras do iOS.
> - Observe que a migração simplesmente alternaria a classe UIWebView com WKWebView, não há trabalho específico a ser feito em relação ao Adobe implicaria o AccessEnabler.


</br>

## Atualizar configurações da build {#update}

Esta versão contém a funcionalidade escrita no idioma SWIFT. Se o aplicativo for totalmente Objetive-C, será necessário definir a caixa de seleção &quot;Sempre integrar bibliotecas padrão Swift&quot; nas configurações de criação do seu público-alvo como &quot;Sim&quot;. Quando essa opção é definida, o Xcode verifica as estruturas agrupadas no aplicativo e, se qualquer uma delas contiver código Swift, ele copiará as bibliotecas pertinentes no pacote do aplicativo. Se você não atualizar as configurações de criação, seu aplicativo poderá falhar com erros informando que não pode carregar AccessEnabler.framework ou vários `ibswift*` bibliotecas.

</br>

## Adicionar sua declaração de software {#add}

> Para obter informações sobre como obter sua declaração de software, acesse este tópico
> página:
> [Registro do aplicativo](/help/authentication/iostvos-application-registration.md)

Depois de ter sua declaração de software, recomendamos hospedá-la em um servidor remoto para que você possa revogá-la facilmente ou alterá-la ao implantar uma nova versão do aplicativo no App Store. Quando o aplicativo for iniciado, obtenha sua instrução de software do local remoto e transmita-a no construtor AccessEnabler:

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> Informações da API aqui: [Referência da API do iOS / tvOS](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Adicionar o esquema de URL personalizado {#add-custom}

> Para obter informações sobre como obter um esquema de URL personalizado, acesse esta página: [Obter um esquema de URL do cliente](/help/authentication/iostvos-application-registration.md)

Após obter o esquema de URL personalizado, é necessário adicioná-lo ao arquivo info.plist do aplicativo. O esquema personalizado tem este formato: `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. Você precisa omitir o sinal de dois pontos e as barras ao adicioná-lo ao arquivo. O exemplo acima se tornará `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>
```

</br>

## Interceptar chamadas no esquema de URL personalizado {#intercept}

Isso se aplica somente no caso de seu aplicativo habilitado anteriormente como Manipulação manual do Safari View Controller (SVC) por meio do [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) e para MVPDs específicos que exigem o Safari View Controller (SVC), portanto exigindo o carregamento dos URLs dos endpoints de autenticação e logout por um controlador SFSafariViewController em vez de um controlador UIWebView/WKWebView.

Durante os fluxos de autenticação e logout, o aplicativo deve monitorar a atividade do `SFSafariViewController `à medida que passa por vários redirecionamentos. Seu aplicativo deve detectar o momento em que carrega um URL personalizado específico definido por seu `application's custom URL scheme` (por exemplo,`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. Quando o controlador carrega esse URL personalizado específico, seu aplicativo deve fechar o `SFSafariViewController` e faça uma chamada para AccessEnabler `handleExternalURL:url `Método da API.

Em seu `AppDelegate` adicione o seguinte método:

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> Informações da API aqui: [Gerenciar URL externo](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Atualizar a assinatura do método setRequestor {#update-setreq}

Como o novo SDK está usando um novo mecanismo de autenticação, não há necessidade do parâmetro signedRequestId ou da chave pública e do segredo (para tvOS). O `setRequestor` O método é simplificado e precisa apenas da requestorID.

### iOS

Este código:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

torna-se:

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

Este código:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

torna-se:

```swift
    accessEnabler.setRequestor(requestorId)
```

> Informações da API aqui: [Definir Solicitante](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Substitua o método getAuthenticationToken pelo método handleExternalURL {#replace}

`getAuthentication` foi usado anteriormente para concluir o fluxo de autenticação. Como o nome era enganoso, ele foi renomeado para `handleExternalURL` O e o pega o url como parâmetro.

Altere todas as ocorrências desta opção:

```swift
    accessEnabler.getAuthenticationToken()
```

neste contexto:

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> Informações da API aqui: [Gerenciar URL externo](/help/authentication/iostvos-sdk-api-reference.md)
