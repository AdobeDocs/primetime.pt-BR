---
seo-title: Usar identificadores de máquina
title: Usar identificadores de máquina
uuid: 14eee414-62f1-4a9d-84bd-689ca2271d19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usar identificadores de máquina{#use-machine-identifiers}

Todas as solicitações do Adobe Primetime DRM (com exceção das solicitações que oferecem suporte à compatibilidade do FMRMS) incluem informações sobre o token do computador que foi emitido para o cliente durante a individualização. O token de máquina inclui uma ID de máquina, que é um identificador que foi atribuído durante a individualização. Você pode usar esse identificador para contar o número de computadores dos quais um usuário solicitou uma licença ou ingressou em um domínio.

Você pode usar um identificador da seguinte maneira:

* O método `getUniqueId()` retorna uma string que foi atribuída a um dispositivo durante a individualização. É possível armazenar as strings em um banco de dados e pesquisar por identificador. No entanto, esse identificador muda se o usuário reformata o disco rígido e se individualiza novamente. Esse identificador também tem um valor diferente entre o Adobe AIR e o Flash Player Adobe em navegadores diferentes na mesma máquina.
* Se quiser contar máquinas com mais precisão, você pode usar `getBytes()` para armazenar o identificador inteiro. Para determinar se a máquina foi vista antes, obtenha todos os identificadores de um nome de usuário e chame `matches()` para verificar se há alguma correspondência. Como o método `matches()` deve ser usado para comparar os valores retornados por `MachineId.getBytes`, essa opção só é prática quando há um pequeno número de valores a serem comparados; por exemplo, as máquinas associadas a um usuário específico.

