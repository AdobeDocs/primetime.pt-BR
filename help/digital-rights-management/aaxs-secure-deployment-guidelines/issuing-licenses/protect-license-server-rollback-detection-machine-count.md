---
title: Contagem de máquinas ao emitir licenças
description: Contagem de máquinas ao emitir licenças
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Contagem de máquinas ao emitir licenças{#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o Servidor de licenças ou o Servidor de domínio deverá armazenar as IDs da máquina associadas ao usuário. A maneira mais eficiente de rastrear IDs de máquina é armazenar o valor retornado pela variável `MachineId.getBytes()` em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs de máquina conhecidas usando `MachineId.matches()`.

`MachineId.matches()` O executa uma comparação de IDs para determinar se elas representam a mesma máquina. Essa comparação só será prática se houver um pequeno número de IDs de máquina para comparação. Por exemplo, se um usuário tiver permissão para cinco máquinas em seu domínio, você poderá pesquisar no banco de dados as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

>[!NOTE]
>
>Essa comparação não é prática para implantações que permitem acesso anônimo. Nesses casos, `MachineId.getUniqueID()` pode ser usada, no entanto, essa ID não será a mesma se o usuário acessar o conteúdo dos tempos de execução do Flash e do Adobe AIR® e não sobreviverá se o usuário reformatar o disco rígido.

Para saber mais sobre `MachineToken.getMachineId()`e `MachineId.matches()`, consulte o *Referência da API de acesso do Adobe*.
