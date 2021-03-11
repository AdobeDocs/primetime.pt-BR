---
title: Uso de identificadores de máquina
description: Uso de identificadores de máquina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Usando identificadores de máquina{#using-machine-identifiers}

Todas as solicitações de acesso ao Adobe (com exceção das solicitações que oferecem suporte à compatibilidade com o FMRMS) contêm informações sobre o token do computador emitido ao cliente durante a individualização. O token da máquina contém uma ID da máquina, um identificador atribuído durante a individualização. Use esse identificador para contar o número de máquinas das quais um usuário solicitou uma licença ou ingressou em um domínio.

Há duas maneiras de usar o identificador. O método `getUniqueId()` retorna uma string atribuída ao dispositivo durante a individualização. Você pode armazenar as cadeias de caracteres em um banco de dados e pesquisar por identificador. No entanto, esse identificador será alterado se o usuário reformatar o disco rígido e se individualizar novamente. Esse identificador também terá um valor diferente entre o Adobe® AIR® e o Flash® Player do Adobe® em navegadores diferentes na mesma máquina.

Para contar máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista anteriormente, obtenha todos os identificadores de um nome de usuário e chame `matches()` para verificar se há correspondência. Como o método `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`, essa opção só é prática quando há um pequeno número de valores para comparar (por exemplo, as máquinas associadas a um usuário específico).
