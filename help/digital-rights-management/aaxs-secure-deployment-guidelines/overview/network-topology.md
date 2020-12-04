---
seo-title: Visão geral da topologia de rede
title: Visão geral da topologia de rede
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Visão geral da topologia de rede {#network-topology-overview}

Depois que você implantar com êxito o Acesso ao Adobe, é importante manter a segurança do seu ambiente. Esta seção descreve as tarefas necessárias para manter a segurança do servidor de produção do Adobe Access.

Use um *proxy reverso* para garantir que diferentes conjuntos de URLs para aplicativos da Web de Acesso ao Adobe estejam disponíveis para usuários externos e internos. Essa configuração é mais segura do que permitir que os usuários se conectem diretamente ao servidor de aplicativos no qual o Adobe Access está sendo executado. O proxy reverso executa todas as solicitações HTTP para o servidor de aplicativos que está executando o Adobe Access. Os usuários só têm acesso de rede ao proxy reverso e podem tentar somente as conexões de URL suportadas pelo proxy reverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

