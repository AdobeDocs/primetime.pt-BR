---
title: Usar identificadores de máquina
description: Usar identificadores de máquina
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usar identificadores de máquina{#use-machine-identifiers}

Todas as solicitações do Adobe Primetime DRM (com exceção das solicitações que oferecem suporte à compatibilidade do FMRMS) incluem informações sobre o token do computador emitido para o cliente durante a individualização. O token do computador inclui uma ID de computador, que é um identificador atribuído durante a individualização. Você pode usar esse identificador para contar o número de computadores dos quais um usuário solicitou uma licença ou ingressou em um domínio.

Você pode usar um identificador da seguinte maneira:

* A variável `getUniqueId()` O método retorna uma string que foi atribuída a um dispositivo durante a individualização. Você pode armazenar as cadeias de caracteres em um banco de dados e pesquisar por identificador. No entanto, esse identificador será alterado se o usuário reformatar o disco rígido e individualizar novamente. Esse identificador também tem um valor diferente entre o Adobe AIR Adobe e o Flash Player em navegadores diferentes na mesma máquina.
* Se quiser contar as máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista antes, obtenha todos os identificadores para um nome de usuário e chame `matches()` para verificar se há correspondência. Como a variável `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`No entanto, essa opção só é prática quando há um pequeno número de valores para comparar; por exemplo, as máquinas associadas a um usuário específico.

