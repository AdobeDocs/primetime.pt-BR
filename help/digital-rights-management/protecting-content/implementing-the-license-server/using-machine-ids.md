---
title: Usar identificadores de máquina
description: Usar identificadores de máquina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usar identificadores de máquina{#use-machine-identifiers}

Todas as solicitações de DRM da Adobe Primetime (com exceção das solicitações que oferecem suporte à compatibilidade com o FMRMS) incluem informações sobre o token do computador que foi emitido para o cliente durante a individualização. O token da máquina inclui uma ID da máquina, que é um identificador que foi atribuído durante a individualização. Você pode usar esse identificador para contar o número de máquinas das quais um usuário solicitou uma licença ou ingressou em um domínio.

Você pode usar um identificador da seguinte maneira:

* O método `getUniqueId()` retorna uma string que foi atribuída a um dispositivo durante a individualização. Você pode armazenar as cadeias de caracteres em um banco de dados e pesquisar por identificador. No entanto, esse identificador é alterado se o usuário reformata o disco rígido e se individualiza novamente. Esse identificador também tem um valor diferente entre o Adobe AIR e o Flash Player de Adobe em navegadores diferentes na mesma máquina.
* Se quiser contar máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista anteriormente, obtenha todos os identificadores de um nome de usuário e chame `matches()` para verificar se há correspondência. Como o método `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`, essa opção só é prática quando há um pequeno número de valores para comparar; por exemplo, as máquinas associadas a um usuário específico.

