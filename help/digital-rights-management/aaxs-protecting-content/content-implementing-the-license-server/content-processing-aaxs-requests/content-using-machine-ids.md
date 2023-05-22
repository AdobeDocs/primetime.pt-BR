---
title: Utilização de identificadores de máquina
description: Utilização de identificadores de máquina
copied-description: true
exl-id: 61ff9240-0c29-437e-b676-7983e2cc5f7b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Utilização de identificadores de máquina{#using-machine-identifiers}

Todas as solicitações de Acesso ao Adobe (com exceção das solicitações que oferecem suporte à compatibilidade FMRMS) contêm informações sobre o token do computador emitido para o cliente durante a individualização. O token do computador contém uma ID de computador, um identificador atribuído durante a individualização. Use esse identificador para contar o número de computadores dos quais um usuário solicitou uma licença ou ingressou em um domínio.

Há duas maneiras de usar o identificador. A variável `getUniqueId()` O método retorna uma string atribuída ao dispositivo durante a individualização. Você pode armazenar as cadeias de caracteres em um banco de dados e pesquisar por identificador. No entanto, esse identificador será alterado se o usuário reformatar o disco rígido e individualizar novamente. Esse identificador também terá um valor diferente entre o Adobe® AIR® e o Adobe® Flash® Player em navegadores diferentes na mesma máquina.

Para contar máquinas com mais precisão, é possível usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista antes, obtenha todos os identificadores para um nome de usuário e chame `matches()` para verificar se há correspondência. Como a variável `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`No entanto, essa opção só é prática quando há um pequeno número de valores para comparar (por exemplo, as máquinas associadas a um usuário específico).
