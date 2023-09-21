---
title: Armazenando políticas com segurança
description: Armazenando políticas com segurança
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Armazenando políticas com segurança{#securely-storing-policies}

O SDK de acesso do Adobe oferece grande flexibilidade no desenvolvimento de aplicativos para uso em pacotes de conteúdo e criação de políticas. Ao criar esses aplicativos, talvez você queira permitir que alguns usuários criem e modifiquem políticas e limitar outros usuários de modo que eles só possam aplicar políticas existentes ao conteúdo. Se esse for o caso, você deverá implementar os controles de acesso necessários para criar contas de usuário com privilégios diferentes para a criação de políticas e a aplicação de políticas ao conteúdo.

As políticas não são assinadas ou protegidas contra modificações até que sejam usadas na embalagem. Se você estiver preocupado com os usuários das ferramentas de empacotamento que modificam políticas, considere assinar as políticas para garantir que elas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos usando o SDK, consulte a *Referência da API de acesso do Adobe*.
