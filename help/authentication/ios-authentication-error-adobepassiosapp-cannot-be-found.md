---
title: Erro de Autenticação do iOS - não é possível encontrar adobepass.ios.app
description: Erro de Autenticação do iOS - não é possível encontrar adobepass.ios.app
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Erro de Autenticação do iOS - não é possível encontrar adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Problema {#issue}

O usuário está passando pelo fluxo de Autenticação e, depois de ter inserido com sucesso suas credenciais com seu provedor, ele é redirecionado para uma página de erro, uma página de pesquisa ou alguma outra página personalizada informando que `adobepass.ios.app` não foi possível localizar/resolver.

## Explicação {#explanation}

No iOS, `adobepass.ios.app` é usada como a URL de redirecionamento final para indicar que o fluxo de AuthN foi concluído. Neste ponto, o aplicativo precisa fazer uma solicitação ao AccessEnabler para obter o Token AuthN e finalizar o fluxo AuthN.

O problema é que `adobepass.ios.app` na verdade não existe e acionará uma mensagem de erro no `webView`. Versões anteriores do DemoApp do iOS presumiam que esse erro sempre seria acionado no final do fluxo do AuthN e era configurado para gerenciá-lo adequadamente (`indidFailLoadWithError`).

**Observação:** Esse problema foi corrigido em versões posteriores do DemoApp (incluído no download do SDK do iOS).

Infelizmente, este pressuposto NÃO está correto. Há alguns servidores DNS ou Proxy &quot;inteligentes&quot; que não transmitem simplesmente o erro gerado, mas executam um dos seguintes procedimentos: 

- Criar uma página de erro personalizada
- Encaminhar para uma página de pesquisa ou para algum outro tipo de página ou portal do cliente.

Nesses casos, a resposta que retornar ao iOS webView será uma resposta perfeitamente válida no que diz respeito ao webView e NÃO acionará o erro que o DemoApp antigo dependia.

## Solução {#solution}

NÃO faça a mesma suposição que o DemoApp faz. Em vez disso, intercepte a solicitação antes que ela seja executada (em `shouldStartLoadWithRequest`) e manuseá-la adequadamente.

Exemplo de como interceptar a solicitação antes de ser executada:

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

Algumas observações:

- NUNCA use `adobepass.ios.app` diretamente em qualquer lugar no código. Em vez disso, use a constante `ADOBEPASS_REDIRECT_URL`
- O `return NO;` impedirá o carregamento da página
- Certifique-se de que a variável `getAuthenticationToken` chamada é chamada uma vez e somente uma vez no código. Várias chamadas para `getAuthenticationToken` resultará em resultados indefinidos.

