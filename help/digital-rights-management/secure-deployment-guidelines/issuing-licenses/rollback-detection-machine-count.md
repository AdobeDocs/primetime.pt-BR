---
description: Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o Servidor de licenças ou o Servidor de domínio deverá armazenar as IDs de máquina associadas ao usuário.
title: Contagem de máquinas ao emitir licenças
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Contagem de máquinas ao emitir licenças {#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o Servidor de licenças ou o Servidor de domínio deverá armazenar as IDs de máquina associadas ao usuário.

A maneira mais eficiente de rastrear IDs de máquina é armazenar o valor retornado pela variável [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs de máquina conhecidas usando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) O executa uma comparação de IDs para determinar se as IDs representam a mesma máquina. Essa comparação só será prática se houver um pequeno número de IDs de máquina. Por exemplo, se os usuários tiverem permissão para cinco máquinas em seu domínio, você poderá pesquisar no banco de dados as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

Essa comparação não é prática para implantações que permitem acesso anônimo. Nesse caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) pode ser usado. No entanto, essa ID não pode ser a mesma se o usuário acessar o conteúdo do Flash e do Adobe AIR® Runtimes.

>[!NOTE]
>
>A ID não sobrevive se o usuário reformatar o disco rígido.