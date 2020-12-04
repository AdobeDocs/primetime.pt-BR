---
seo-title: Contagem de máquina ao emitir licenças
title: Contagem de máquina ao emitir licenças
uuid: d57f8b0b-0363-4b26-bd71-76f4abe5b68f
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Contagem de máquina ao emitir licenças{#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs de máquina associadas ao usuário. A maneira mais robusta de rastrear IDs de máquina é armazenar o valor retornado pelo método `MachineId.getBytes()` em um banco de dados. Quando uma nova solicitação entrar, compare a ID da máquina na solicitação com as IDs de máquina conhecidas usando `MachineId.matches()`.

`MachineId.matches()` realiza uma comparação de IDs para determinar se representam a mesma máquina. Essa comparação só é prática se houver um pequeno número de IDs de máquina para comparação. Por exemplo, se um usuário tiver permissão para cinco computadores dentro de seu domínio, você poderá pesquisar no banco de dados as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

>[!NOTE]
>
>Essa comparação não é prática para implantações que permitem acesso anônimo. Nesses casos, `MachineId.getUniqueID()` pode ser usado, no entanto, essa ID não será a mesma se o usuário acessar o conteúdo dos tempos de execução do Flash e do Adobe AIR® e não sobreviverá se o usuário reformatar seu disco rígido.

Para saber mais sobre `MachineToken.getMachineId()`e `MachineId.matches()`, consulte *Referência da API de Acesso ao Adobe*.
