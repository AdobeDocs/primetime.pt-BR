---
title: Atualizar o banco de dados de implementação de referência
description: Atualizar o banco de dados de implementação de referência
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Atualizar a implementação de referência DB{#update-the-reference-implementation-db}

Para controlar os modelos de uso sob os quais uma licença é emitida para um usuário designado, adicione entradas ao banco de dados de implementação de referência.

1. Adicione entradas à tabela `Customer`.

   A tabela `Customer` inclui nomes de usuário e senhas para autenticar usuários. Também indica se um usuário tem uma assinatura (uma licença emitida sob o modelo de uso *Subscription*).

1. Conceda acesso a um usuário nos modelos de uso Download para o proprietário ou Vídeo sob demanda.

       Adicione entradas à tabela &quot;CustomerAuthorization&quot; para especificar:
   
   * O modelo de uso
   * Cada segmento de conteúdo que um usuário pode acessar

Para obter mais informações sobre como preencher cada tabela, consulte o script [!DNL PopulateSampleDB.sql] (incluído em seu DVD DRM do Primetime no diretório [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]).
