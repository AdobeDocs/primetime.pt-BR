---
seo-title: Implementação da visão geral dos modelos de uso
title: Implementação da visão geral dos modelos de uso
uuid: 1041bb84-9996-4284-b2a0-d6fc6d4b73d9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Implementação da visão geral dos modelos de uso {#implementing-the-usage-models-overview}

A Implementação de referência inclui uma lógica de negócios para demonstrar como ativar os quatro modelos diferentes a seguir para um conteúdo empacotado:

* Download por conta própria (DTO)
* Aluguer/VOD (Video-on-demand)
* Subscrição (tudo o que você pode comer)
* Financiamento de anúncios

Para habilitar a demonstração do modelo de uso, especifique a propriedade personalizada `RI_UsageModelDemo=true` no momento do empacotamento. Se você estiver empacotando conteúdo usando a ferramenta de linha de comando Media Packager, especifique:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licenças usará a política especificada no momento do empacotamento para emitir uma licença. Se várias políticas forem especificadas, o servidor de licenças usará a primeira política válida.

Na demonstração, a lógica comercial no servidor controla os atributos reais das licenças geradas. No momento da embalagem, apenas as informações mínimas de política devem ser incluídas no conteúdo. Especificamente, a política precisa apenas indicar se a autenticação é necessária para acessar o conteúdo. Para habilitar todos os quatro modelos de uso, inclua uma política que permita acesso anônimo (para o modelo financiado pelo anúncio) e uma política que exija autenticação de nome de usuário/senha (para os outros três modelos de uso). Ao solicitar uma licença, um aplicativo cliente pode determinar se deseja solicitar a autenticação do usuário com base nas informações de autenticação nas políticas.

Para controlar o modelo de utilização ao abrigo do qual um determinado utilizador deve receber uma licença, podem ser acrescentadas entradas à base de dados de implementação de referência. A `Customer` tabela contém nomes de usuários e senhas para autenticação de usuários. Também indica se o usuário tem uma subscrição. Os usuários com subscrição receberão licenças sob o modelo de uso da *Subscrição* . Para conceder acesso a um usuário nos modelos de uso *Download para* próprio ou *Vídeo sob demanda* , uma entrada pode ser adicionada à `CustomerAuthorization` tabela, que especifica cada parte do conteúdo que o usuário tem permissão para acessar e o modelo de uso. Consulte o [!DNL PopulateSampleDB.sql] script para obter detalhes sobre como preencher cada tabela.

Quando um usuário solicita uma licença, o servidor de Implementação de referência verifica os metadados enviados pelo cliente para determinar se o conteúdo foi empacotado usando a `RI_UsageModelDemo` propriedade. Em caso afirmativo, são usadas as seguintes regras de negócios:

* Se uma das políticas exigir autenticação:

   * Se a solicitação contiver um token de autenticação válido, procure o usuário na tabela do banco de dados Cliente. Se o usuário foi encontrado:

      * Se a `Customer.IsSubscriber` propriedade for `true`, gere uma licença para o modelo de uso da *Subscrição* e envie-a ao usuário.

      * Procure um registro na tabela do `CustomerAuthorization` banco de dados para esse usuário e ID de conteúdo. Se um registro foi encontrado:

         * Se `CustomerAuthorization.UsageType` for `DTO`, gere uma licença para o modelo de uso *Baixar para* o proprietário e envie-a para o usuário.

         * Se `CustomerAuthorization.UsageType` for `VOD`, gere uma licença para o modelo de uso do *Video On Demand* e envie-a ao usuário.
   * Se nenhuma das políticas permitir acesso anônimo:

      * Se não houver um token de autenticação válido na solicitação, retorne um erro de &quot;autenticação obrigatória&quot;.
      * Caso contrário, retorne um erro &quot;não autorizado&quot;.


* Se uma das políticas permitir acesso anônimo, gere uma licença para o modelo de uso financiado pelo anúncio e envie-a ao usuário.

Antes que o servidor de Implementação de referência possa emitir licenças para a demonstração do modelo de uso, o servidor precisa ser configurado para especificar como as licenças são geradas para cada um dos quatro modelos de uso. Isso é feito especificando uma política para cada modelo de uso. A Implementação de referência inclui quatro exemplos de políticas ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) ou você pode substituir suas próprias políticas. Em [!DNL flashaccess-refimpl.properties], defina as seguintes propriedades para especificar a política a ser usada para cada modelo de uso e coloque os arquivos de política no diretório especificado pela `config.resourcesDirectory` propriedade:

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

