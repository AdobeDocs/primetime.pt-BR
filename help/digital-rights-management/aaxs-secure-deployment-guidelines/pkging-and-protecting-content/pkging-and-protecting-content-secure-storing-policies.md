---
title: Armazenando políticas com segurança
description: Armazenando políticas com segurança
copied-description: true
exl-id: fd335a0c-7eb1-4159-958f-7302fce98cef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Armazenando políticas com segurança{#securely-storing-policies}

O SDK de acesso do Adobe oferece grande flexibilidade no desenvolvimento de aplicativos para uso em pacotes de conteúdo e criação de políticas. Ao criar esses aplicativos, talvez você queira permitir que alguns usuários criem e modifiquem políticas e limitar outros usuários de modo que eles só possam aplicar políticas existentes ao conteúdo. Se esse for o caso, você deverá implementar os controles de acesso necessários para criar contas de usuário com privilégios diferentes para a criação de políticas e a aplicação de políticas ao conteúdo.

As políticas não são assinadas ou protegidas contra modificações até que sejam usadas na embalagem. Se você estiver preocupado com os usuários das ferramentas de empacotamento que modificam políticas, considere assinar as políticas para garantir que elas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos usando o SDK, consulte a *Referência da API de acesso do Adobe*.
