---
seo-title: Lista de permissões de aplicativos não SWF
title: Lista de permissões de aplicativos não SWF
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Lista de permissões de aplicativos não SWF {#non-swf-application-whitelisting}

O AIR foi a primeira plataforma que apresentou a lista de permissões do aplicativo e o nome da propriedade que você usa para adicionar aplicativos não SWF à lista de permissões (Adobe AIR, iOS, Android etc.) mantém seu nome original: `policy.allowedAIRApplication.n`. Isso permite que o conteúdo seja reproduzido por todos os aplicativos não Flash assinados com um Certificado de assinatura antes da publicação. Isso é conhecido como o *ID da aplicação*. Você pode extrair a ID da aplicação usando a [!DNL AdobePublisherIDUtility.jar] ferramenta. Esta lista de permissões será aplicada a qualquer cliente que suporte o Primetime DRM.

O ID da aplicação é derivado da chave pública do certificado de assinatura usado para assinar um determinado aplicativo. Se a chave pública no certificado expirar, todo o conteúdo anterior exibido na lista de permissões será reproduzido somente em aplicativos assinados com o certificado antigo não será reproduzido no novo aplicativo (assinado com o novo certificado).

Se você estiver em uma situação em que uma biblioteca de conteúdo é listada em whitelist para aplicativos que foram assinados com um certificado de assinatura específico e esse certificado expirar e você receber um novo certificado (com um par de chaves público/privado diferente), seu conteúdo antigo não será reproduzido no seu novo aplicativo, a *menos* que você execute um dos procedimentos a seguir:

* Use um `PolicyUpdateList` no servidor de licenças para substituir a política de entrada e inserir uma nova entrada da Lista de permissões do aplicativo com o resumo do seu novo certificado de assinatura.
* Atualize a lógica do servidor de licenças para substituir a política de entrada e insira uma nova entrada da Lista de permissões do aplicativo.
* Solicite que o emissor do certificado de assinatura emita um novo certificado que use o mesmo par de chaves público/privado usado pelo certificado anterior.
* Se você estiver fornecendo conteúdo HDS/HLS que esteja referenciando um ponto final de URL para recuperar o `DRMMetadata`, poderá gerar novamente o `DRMMetadata` (usando o SDK Java DRM Primetime) para inserir uma nova Política DRM que contenha uma entrada atualizada da Lista de permissões do aplicativo.

* Recoloque todo o seu conteúdo antigo com uma nova política de DRM que tenha a compilação do seu novo certificado de assinatura.

Consulte `policy.allowedAIRApplication.n` nas propriedades ** de configuração para obter detalhes.

>[!NOTE]
>
>Permitir a listagem de um aplicativo iOS requer uma abordagem especial. Consulte [Permitir listar seu aplicativo](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) iOS no Guia *do Programador do* TVSDK para iOS.
