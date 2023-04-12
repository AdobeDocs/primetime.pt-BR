---
title: Suporte SFSafariViewController no iOS SDK 3.2+
description: Suporte SFSafariViewController no iOS SDK 3.2+
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Suporte SFSafariViewController no iOS SDK 3.2+ {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>


**Devido a requisitos de segurança, algumas páginas de logon do MVPD DEVEM ser apresentadas em um SFSafariViewController, em vez de visualizações da Web.**

Alguns MVPDs exigem que suas páginas de logon sejam apresentadas em um controle de navegador seguro, como SFSafariViewController. Eles estão bloqueando ativamente as visualizações da Web, portanto, para poder autenticar com eles, devemos usar o SVC. 

## Compatibilidade {#compatiblity}

A partir do iOS SDK versão 3.1, o AccessEnabler SDK exibe automaticamente a página de logon de MVPDs específicos em um SFSafariViewController, com base na configuração do servidor.

A versão 3.1 do SDK apresenta automaticamente o SFSafariViewController do controlador de visualização raiz do aplicativo. Embora isso simplifique o gerenciamento de páginas de logon para implementadores, há casos em que a apresentação do SFSafariViewController a partir do controlador de visualização raiz não é possível, devido à implementação específica do aplicativo (como um controlador modal já visível).

Nesses casos, a versão 3.2 introduz a capacidade do programador gerenciar manualmente o SVC.

## Gerenciamento manual de VPC {#manual-svc-management}

Para gerenciar manualmente o SVC, o implementador deve executar as seguintes etapas:
 

1. chamada **setOptions([&quot;handleSVC&quot;:true])** após a inicialização do AccessEnabler (verifique se essa chamada é executada antes do início da autenticação). Isso habilitará o gerenciamento &quot;manual&quot; de SVC, o SDK não apresentará automaticamente o SVC, mas, quando necessário, chamará **navegue(toUrl:*{url}* useSVC:true)**.  

1. implementar o retorno de chamada opcional **navigateToUrl:useSVC:** dentro da implementação, você deve criar uma instância svc usando a instância SFSafariViewController usando o url fornecido e apresentá-lo na tela:

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***Notas:***

   - *Você pode personalizar o SFSafariViewController da maneira que desejar. Por exemplo, no iOS 11+, você pode alterar o rótulo &quot;Concluído&quot; para &quot;Cancelar&quot;.*
   - *para poder descartar o svc, você precisa de uma referência a ele, não crie no escopo de **navigateToUrl:useSVC***
   - *use seu próprio controlador de exibição para &quot;myController&quot;*\
       

1. Na implementação delegada do aplicativo de **application(\_app: UIApplication, abrir url: URL, opções: \[UIApplicationOpenURLOoptionsKey: Qualquer\]) -\> Bool**, adicione o código para fechar o svc. Você já deve ter algum código lá que chame **accessEnabler.handleExternalURL()**. Logo abaixo adicione:

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   Novamente, svc é uma referência ao SFSafariViewController que você criou na etapa 2.\
    

1. Implementar **safariViewControllerDidFinish(\_ controlador: SFSafariViewController)** from **SFSafariViewControllerDelegate** para capturar quando o usuário cancelou o svc usando o botão &quot;Concluído&quot;. Nesta função, para informar ao SDK que a autenticação foi cancelada, é necessário chamar:

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```

