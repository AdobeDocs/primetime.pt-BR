---
title: Armazenamento seguro de políticas
description: Armazenamento seguro de políticas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Armazenamento seguro de políticas{#securely-storing-policies}

O SDK do Adobe Access oferece uma grande flexibilidade no desenvolvimento de aplicativos para uso em pacotes de conteúdo e criação de políticas. Ao criar esses aplicativos, você pode permitir que alguns usuários criem e modifiquem políticas e limitar outros usuários, de modo que eles possam aplicar somente as políticas existentes ao conteúdo. Se esse for o caso, você deverá implementar os controles de acesso necessários para criar contas de usuário com privilégios diferentes para a criação de política e a aplicação de políticas ao conteúdo.

As políticas não são assinadas ou protegidas de qualquer outra forma contra modificações até serem usadas em embalagens. Se estiver preocupado com os usuários de suas ferramentas de empacotamento que modificam políticas, considere assinar as políticas para garantir que elas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos usando o SDK, consulte a *Referência da API de acesso ao Adobe*.
