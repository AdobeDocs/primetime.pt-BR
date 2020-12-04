---
description: Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs de máquina associadas ao usuário.
seo-description: Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs de máquina associadas ao usuário.
seo-title: Contagem de máquina ao emitir licenças
title: Contagem de máquina ao emitir licenças
uuid: 7ba8a8d4-a31f-4f37-82a7-755cfa443544
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Contagem de máquina ao emitir licenças {#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs de máquina associadas ao usuário.

A maneira mais robusta de rastrear IDs de máquina é armazenar o valor retornado pelo método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs da máquina conhecidas usando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza uma comparação de IDs para determinar se as IDs representam a mesma máquina. Essa comparação só é prática se houver um pequeno número de IDs de máquina. Por exemplo, se os usuários tiverem cinco computadores em seus domínios, você poderá pesquisar no banco de dados as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

Essa comparação não é prática para implantações que permitem acesso anônimo. Nesse caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) pode ser usado. No entanto, essa ID não pode ser a mesma se o usuário acessar o conteúdo dos tempos de execução do Flash e do Adobe AIR®.

>[!NOTE]
>
>A ID não sobrevive se o usuário reformatar o disco rígido.