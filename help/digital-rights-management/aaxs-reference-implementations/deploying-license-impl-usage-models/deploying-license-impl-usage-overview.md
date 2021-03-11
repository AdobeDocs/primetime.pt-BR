---
title: Implementar a visão geral dos modelos de uso
description: Implementar a visão geral dos modelos de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Implementar a visão geral dos modelos de uso {#implementing-the-usage-models-overview}

A Implementação de referência inclui lógica comercial para demonstrar como ativar os quatro modelos de uso diferentes a seguir para um conteúdo empacotado:

* Download por conta própria (DTO)
* Aluguer/Vídeo sob demanda (VOD)
* Assinatura (tudo o que você pode comer)
* Financiamento de anúncios

Para habilitar a demonstração do modelo de uso, especifique a propriedade personalizada `RI_UsageModelDemo=true` no momento do empacotamento. Se estiver empacotando conteúdo usando a ferramenta de linha de comando do Media Packager, especifique:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licenças usará a política especificada no momento do empacotamento para emitir uma licença. Se várias políticas foram especificadas, o servidor de licenças usará a primeira política válida.

Na demonstração, a lógica de negócios no servidor controla os atributos reais das licenças geradas. No momento da embalagem, apenas as informações políticas mínimas devem ser incluídas no conteúdo. Especificamente, a política só precisa indicar se a autenticação é necessária para acessar o conteúdo. Para habilitar todos os quatro modelos de uso, inclua uma política que permita acesso anônimo (para o modelo financiado pelo anúncio) e uma política que exija autenticação de nome de usuário/senha (para os outros três modelos de uso). Ao solicitar uma licença, um aplicativo cliente pode determinar se deseja solicitar a autenticação do usuário com base nas informações de autenticação nas políticas.

Para controlar o modelo de utilização ao abrigo do qual um determinado utilizador deve receber uma licença, podem ser acrescentadas entradas à base de dados de Implementação de Referência. A tabela `Customer` contém nomes de usuário e senhas para autenticação de usuários. Também indica se o usuário tem uma assinatura. Os usuários com assinaturas receberão licenças sob o modelo de uso *Subscription*. Para conceder acesso a um usuário nos modelos de uso *Baixar para Próprio* ou *Vídeo sob Demanda*, uma entrada pode ser adicionada à tabela `CustomerAuthorization`, que especifica cada parte do conteúdo que o usuário tem permissão para acessar e o modelo de uso. Consulte o script [!DNL PopulateSampleDB.sql] para obter detalhes sobre como preencher cada tabela.

Quando um usuário solicita uma licença, o servidor de Implementação de Referência verifica os metadados enviados pelo cliente para determinar se o conteúdo foi empacotado usando a propriedade `RI_UsageModelDemo` . Em caso afirmativo, as seguintes regras de negócios serão usadas:

* Se uma das políticas exigir autenticação:

   * Se a solicitação contiver um token de autenticação válido, procure o usuário na tabela do banco de dados do Cliente. Se o usuário foi encontrado:

      * Se a propriedade `Customer.IsSubscriber` for `true`, gere uma licença para o modelo de uso *Subscription* e a envie para o usuário.

      * Procure um registro na tabela de banco de dados `CustomerAuthorization` desse usuário e ID de conteúdo. Se um registro foi encontrado:

         * Se `CustomerAuthorization.UsageType` for `DTO`, gere uma licença para o modelo de uso *Baixar para próprio* e envie-a para o usuário.

         * Se `CustomerAuthorization.UsageType` for `VOD`, gere uma licença para o modelo de uso *Vídeo sob demanda* e a envie para o usuário.
   * Se nenhuma das políticas permitir acesso anônimo:

      * Se não houver um token de autenticação válido na solicitação, retorne um erro de &quot;autenticação necessária&quot;.
      * Caso contrário, retorne um erro &quot;não autorizado&quot;.


* Se uma das políticas permitir o acesso anônimo, gere uma licença para o modelo de uso financiado pelo anúncio e envie-a ao usuário.

Antes do servidor de Implementação de Referência poder emitir licenças para a demonstração do modelo de uso, o servidor precisa ser configurado para especificar como as licenças são geradas para cada um dos quatro modelos de uso. Isso é feito especificando uma política para cada modelo de uso. A Implementação de referência inclui quatro políticas de exemplo ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) ou você pode substituir suas próprias políticas. Em [!DNL flashaccess-refimpl.properties], defina as seguintes propriedades para especificar a política a ser usada para cada modelo de uso e colocar os arquivos de política no diretório especificado pela propriedade `config.resourcesDirectory`:

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```

