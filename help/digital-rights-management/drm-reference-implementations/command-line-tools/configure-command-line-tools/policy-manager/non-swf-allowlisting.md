---
title: Lista de permissões de aplicativos não-SWF
description: Lista de permissões de aplicativos não-SWF
copied-description: true
exl-id: f33fb0e9-144f-49f8-8da2-8a50aea09456
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Lista de permissões de aplicativos não-SWF {#non-swf-application-isting}

O AIR foi a primeira plataforma a incluir aplicativos na lista de permissões e o nome da propriedade usada para lista de permissões aplicativos não SWF (Adobe AIR, iOS, Android etc.) retém o nome original: `policy.allowedAIRApplication.n`. Isso permite que o conteúdo seja reproduzido por todos os aplicativos que não sejam do Flash e que estejam assinados com um Certificado de autenticação antes da publicação. Esse processo é conhecido como *ID do aplicativo*. Você pode extrair a ID do aplicativo usando a variável [!DNL AdobePublisherIDUtility.jar] ferramenta. Essa lista de permissões será aplicada a qualquer cliente que suporte o Primetime DRM.

A ID do aplicativo é derivada da chave pública do certificado de autenticação usado para assinar um determinado aplicativo. Se a chave pública no certificado expirar, todo o conteúdo anterior permitido listado para reprodução somente em aplicativos assinados com o certificado antigo não será reproduzido no novo aplicativo (assinado com o novo certificado).

Se você estiver em uma situação na qual tem uma biblioteca de permissões de conteúdo listada para aplicativos que foram assinados com um determinado certificado de autenticação, e esse certificado expira e você recebe um novo certificado (com um par de chaves públicas/privadas diferente), seu conteúdo antigo não será reproduzido no novo aplicativo *a menos que* você pode executar um dos seguintes procedimentos:

* Use um `PolicyUpdateList` no servidor de licenças para substituir a política de entrada e inserir uma nova entrada do Application Lista de permissões no resumo do novo certificado de autenticação.
* Atualize a lógica do servidor de licenças para substituir a política recebida e inserir uma nova entrada do Application Lista de permissões.
* Solicite que o emissor do seu certificado de autenticação emita um novo certificado que use o mesmo par de chaves públicas/privadas usado pelo seu certificado anterior.
* Se você estiver fornecendo conteúdo HDS/HLS que faz referência a um endpoint de URL para recuperar o `DRMMetadata`, é possível regenerar a variável `DRMMetadata` (usando o SDK do Java DRM do Primetime) para inserir uma nova Política DRM que contém uma entrada atualizada da Lista de permissões do aplicativo.

* Reempacotar todo o conteúdo antigo com uma nova política DRM que tem o resumo do novo certificado de autenticação.

Consulte `policy.allowedAIRApplication.n` in *Propriedades de configuração* para obter detalhes.

>[!NOTE]
>
>A inclusão de um aplicativo do iOS na lista de permissões requer uma abordagem especial. Consulte [Lista de permissões seu aplicativo iOS](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) no *Guia do programador do TVSDK para iOS*.
