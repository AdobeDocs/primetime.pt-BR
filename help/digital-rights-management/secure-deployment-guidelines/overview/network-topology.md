---
title: Visão geral da topologia de rede
description: Visão geral da topologia de rede
copied-description: true
exl-id: a4737ea3-407a-48fd-ae3e-4df56a4c1812
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Visão geral {#network-topology-overview}

Depois de implantar o Adobe Primetime DRM com êxito, você deve manter a segurança do servidor de produção do Primetime DRM.

>[!NOTE]
>
>O Primetime DRM era anteriormente conhecido como Adobe Access e, antes disso, Flash Access.

Você pode usar um *proxy reverso* para garantir que diferentes conjuntos de URLs para aplicativos Web do Primetime DRM estejam disponíveis para usuários externos e internos. *Proxy reverso* é mais seguro do que permitir que os usuários se conectem diretamente ao servidor de aplicativos no qual o Primetime DRM é executado e essa configuração executa todas as solicitações HTTP para o servidor de aplicativos que executa o Primetime DRM. Os usuários podem acessar somente o proxy reverso e podem tentar somente as conexões de URL compatíveis com o proxy reverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
