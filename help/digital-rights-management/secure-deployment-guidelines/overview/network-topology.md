---
seo-title: Visão geral da topologia de rede
title: Visão geral da topologia de rede
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Visão geral {#network-topology-overview}

Depois de implantar com êxito o Adobe Primetime DRM, é necessário manter a segurança do servidor de produção Primetime DRM.

>[!NOTE]
>
>O Primetime DRM era anteriormente conhecido como Adobe Access e antes disso, Flash Access.

Você pode usar um proxy ** reverso para garantir que diferentes conjuntos de URLs para aplicativos Web DRM Primetime estejam disponíveis para usuários externos e internos. *O proxy* reverso é mais seguro do que permitir que os usuários se conectem diretamente ao servidor de aplicativos no qual o Primetime DRM é executado, e essa configuração executa todas as solicitações HTTP para o servidor de aplicativos que executa o Primetime DRM. Os usuários podem acessar somente o proxy reverso e podem tentar somente as conexões de URL suportadas pelo proxy reverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)