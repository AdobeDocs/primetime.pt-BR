---
title: Atualizar o BD de implementação de referência
description: Atualizar o BD de implementação de referência
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Atualizar o BD de implementação de referência{#update-the-reference-implementation-db}

Para controlar modelos de uso sob os quais uma licença é emitida para um usuário designado, adicione entradas ao banco de dados de implementação de referência.

1. Adicionar entradas à `Customer` tabela.

   A variável `Customer` A tabela inclui nomes de usuário e senhas para autenticar usuários. Também indica se um usuário tem uma assinatura (uma licença emitida sob o *Inscrição* modelo de uso).

1. Conceda acesso a um usuário nos modelos de uso Download por conta própria ou Vídeo sob demanda.

       Adicione entradas à tabela &quot;CustomerAuthorization&quot; para especificar:
   
   * O modelo de uso
   * Cada segmento de conteúdo que um usuário pode acessar

Para obter mais informações sobre como preencher cada tabela, consulte [!DNL PopulateSampleDB.sql] (incluído no seu DVD do Primetime DRM no [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] diretório).
