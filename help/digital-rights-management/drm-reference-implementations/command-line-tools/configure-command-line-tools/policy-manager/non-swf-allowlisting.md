---
title: Lista de permissões de aplicativos não SWF
description: Lista de permissões de aplicativos não SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Lista de permissões de aplicativos não SWF {#non-swf-application-isting}

O AIR foi a primeira plataforma que apresentou a lista de permissões do aplicativo e o nome da propriedade que você usa para lista de permissões aplicativos que não são SWF (Adobe AIR, iOS, Android etc.) mantém seu nome original: `policy.allowedAIRApplication.n`. Isso permite que o conteúdo seja reproduzido por todos os aplicativos que não são do Flash e que são assinados com um Certificado de assinatura antes da publicação. Isso é conhecido como *Application ID*. Você pode extrair a ID do aplicativo usando a ferramenta [!DNL AdobePublisherIDUtility.jar]. Essa lista de permissões será aplicada em qualquer cliente compatível com o Primetime DRM.

A ID do aplicativo é derivada da chave pública do certificado de assinatura usado para assinar um determinado aplicativo. Se a chave pública no certificado expirar, todo o conteúdo anterior permitirá que seja reproduzido somente em aplicativos assinados com o certificado antigo não será reproduzido no novo aplicativo (assinado com o novo certificado).

Se você estiver em uma situação em que uma biblioteca de conteúdo permite listar aplicativos que foram assinados com um certificado de assinatura específico e esse certificado expirar e você receber um novo certificado (com um par de chaves público/privado diferente), o conteúdo antigo não será reproduzido no novo aplicativo *a menos que* você faça o seguinte:

* Use um `PolicyUpdateList` no servidor de licenças para substituir a política de entrada e inserir uma nova entrada de Lista de permissões de Aplicativo com o resumo do novo certificado de assinatura.
* Atualize a lógica do servidor de licenças para substituir a política de entrada e insira uma nova entrada do Application Lista de permissões.
* Solicite que seu emissor do certificado de assinatura emita um novo certificado que use o mesmo par de chaves público/privado usado pelo certificado anterior.
* Se você estiver fornecendo conteúdo HDS/HLS que esteja referenciando um ponto de extremidade de URL para recuperar o `DRMMetadata`, poderá gerar novamente o `DRMMetadata` (usando o SDK Java DRM do Primetime) para inserir uma nova Política DRM que contenha uma entrada atualizada do Application Lista de permissões.

* Reembale todo o conteúdo antigo com uma nova política de DRM que tem o resumo do novo certificado de assinatura.

Consulte `policy.allowedAIRApplication.n` em *Propriedades de configuração* para obter detalhes.

>[!NOTE]
>
>Permitir a listagem de um aplicativo iOS requer uma abordagem especial. Consulte [Lista de permissões seu aplicativo iOS](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) no *TVSDK para Guia do Programador iOS*.
