---
seo-title: Atualizar o DB de implementação de referência
title: Atualizar o DB de implementação de referência
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Atualizar a implementação de referência DB{#update-the-reference-implementation-db}

Para controlar os modelos de uso nos quais uma licença é emitida para um usuário designado, adicione entradas ao banco de dados de implementação de referência.

1. Adicione entradas à tabela `Customer`.

   A tabela `Customer` inclui nomes de usuários e senhas para autenticar usuários. Também indica se um usuário tem uma subscrição (uma licença emitida sob o modelo de uso *Subscrição*).

1. Conceda acesso a um usuário nos modelos de uso Download para o proprietário ou Vídeo sob demanda.

       Adicione entradas à tabela &quot;AutorizaçãoCliente&quot; para especificar:
   
   * O modelo de uso
   * Cada segmento do conteúdo que um usuário pode acessar

Para obter mais informações sobre como preencher cada tabela, consulte o script [!DNL PopulateSampleDB.sql] (incluído no DVD do Primetime DRM no diretório [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]).
