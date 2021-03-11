---
description: Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs do computador associadas ao usuário.
title: Contagem de máquina ao emitir licenças
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Contagem de máquina ao emitir licenças {#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs do computador associadas ao usuário.

A maneira mais robusta de rastrear IDs de máquina é armazenar o valor retornado pelo método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs da máquina conhecidas usando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza uma comparação de IDs para determinar se as IDs representam a mesma máquina. Essa comparação só é prática se houver um pequeno número de IDs de máquina. Por exemplo, se os usuários tiverem permissão para cinco computadores em seus domínios, você poderá pesquisar o banco de dados para as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

Essa comparação não é prática para implantações que permitem acesso anônimo. Nesse caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) pode ser usado. No entanto, essa ID não pode ser a mesma se o usuário acessar o conteúdo do Flash e dos tempos de execução do Adobe AIR®.

>[!NOTE]
>
>A ID não sobrevive se o usuário reformatar o disco rígido.