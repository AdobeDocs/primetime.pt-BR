---
seo-title: Armazenar políticas com segurança
title: Armazenar políticas com segurança
uuid: b1ac236f-6637-46d4-8405-a819d6093314
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Armazenamento seguro de políticas{#securely-storing-policies}

O SDK de acesso ao Adobe oferece uma grande flexibilidade no desenvolvimento de aplicativos para uso em pacotes de conteúdo e criação de políticas. Ao criar esses aplicativos, talvez você queira permitir que alguns usuários criem e modifiquem políticas, além de limitar outros usuários, de modo que eles só possam aplicar políticas existentes ao conteúdo. Se esse for o caso, você deverá implementar os controles de acesso necessários para criar contas de usuário com privilégios diferentes para a criação de políticas e a aplicação de políticas ao conteúdo.

As políticas não são assinadas ou protegidas contra modificação até que sejam usadas em embalagens. Se você estiver preocupado com os usuários de suas ferramentas de empacotamento que modificam políticas, considere assinar as políticas para garantir que elas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos usando o SDK, consulte *Referência da API de acesso ao Adobe*.
