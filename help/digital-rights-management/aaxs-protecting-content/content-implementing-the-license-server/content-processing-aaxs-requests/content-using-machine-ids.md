---
seo-title: Uso de identificadores de máquina
title: Uso de identificadores de máquina
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uso de identificadores de máquina{#using-machine-identifiers}

Todas as solicitações do Adobe Access (com exceção das solicitações que oferecem suporte à compatibilidade FMRMS) contêm informações sobre o token do computador emitido para o cliente durante a individualização. O token da máquina contém uma ID da máquina, um identificador atribuído durante a individualização. Use esse identificador para contar o número de computadores dos quais um usuário solicitou uma licença ou ingressou em um domínio.

Há duas maneiras de usar o identificador. O `getUniqueId()` método retorna uma string atribuída ao dispositivo durante a individualização. É possível armazenar as strings em um banco de dados e pesquisar por identificador. No entanto, esse identificador mudará se o usuário reformatar o disco rígido e se individualizar novamente. Esse identificador também terá um valor diferente entre o Adobe® AIR® e o Adobe® Flash® Player em navegadores diferentes na mesma máquina.

Para contar máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista antes, obtenha todos os identificadores de um nome de usuário e chame `matches()` para verificar se há correspondência. Como o `matches()` método deve ser usado para comparar os valores retornados por `MachineId.getBytes`, essa opção só é prática quando há um pequeno número de valores a serem comparados (por exemplo, as máquinas associadas a um usuário específico).
