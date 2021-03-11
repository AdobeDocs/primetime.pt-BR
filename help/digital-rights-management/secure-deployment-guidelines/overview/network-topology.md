---
title: Visão geral da topologia de rede
description: Visão geral da topologia de rede
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Visão geral {#network-topology-overview}

Depois de implantar com êxito o DRM da Adobe Primetime, é necessário manter a segurança do servidor de produção do DRM do Primetime.

>[!NOTE]
>
>O DRM do Primetime era anteriormente conhecido como Adobe Access e, antes disso, Flash Access.

Você pode usar um *proxy reverso* para garantir que diferentes conjuntos de URLs para aplicativos Web DRM do Primetime estejam disponíveis para usuários externos e internos. *O* proxy reverso é mais seguro do que permitir que os usuários se conectem diretamente ao servidor de aplicativos em que o DRM do Primetime é executado, e essa configuração executa todas as solicitações HTTP para o servidor de aplicativos que executa o DRM do Primetime. Os usuários podem acessar somente o proxy reverso e podem tentar apenas as conexões de URL compatíveis com o proxy reverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)