---
title: Contagem de máquina ao emitir licenças
description: Contagem de máquina ao emitir licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Contagem de máquina ao emitir licenças{#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs de máquina associadas ao usuário. A maneira mais robusta de rastrear IDs de máquina é armazenar o valor retornado pelo método `MachineId.getBytes()` em um banco de dados. Quando uma nova solicitação entrar, compare a ID do computador na solicitação com as IDs do computador conhecidas usando `MachineId.matches()`.

`MachineId.matches()` O executa uma comparação das IDs para determinar se elas representam a mesma máquina. Essa comparação só é prática se houver um pequeno número de IDs de máquina para comparar. Por exemplo, se um usuário tiver permissão para cinco máquinas em seu domínio, você poderá pesquisar o banco de dados para as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

>[!NOTE]
>
>Essa comparação não é prática para implantações que permitem acesso anônimo. Nesses casos, `MachineId.getUniqueID()` pode ser usado, no entanto, essa ID não será a mesma se o usuário acessar o conteúdo tanto do Flash quanto do Adobe AIR® runtimes, e não sobreviverá se o usuário reformatar seu disco rígido.

Para saber mais sobre `MachineToken.getMachineId()`e `MachineId.matches()`, consulte a *Referência da API de acesso ao Adobe*.
