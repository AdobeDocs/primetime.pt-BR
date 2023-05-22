---
title: Implementar a visão geral dos modelos de uso
description: Implementar a visão geral dos modelos de uso
copied-description: true
exl-id: 48e7db54-484f-4c46-9a4e-a51bae7c84b4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Implementar a visão geral dos modelos de uso {#implementing-the-usage-models-overview}

A implementação de referência inclui uma lógica de negócios para demonstrar como ativar os quatro modelos de uso diferentes a seguir para um conteúdo empacotado:

* Download por conta própria (DTO)
* Aluguel/Vídeo sob demanda (VOD)
* Assinatura (tudo o que você pode comer)
* Financiado por anúncio

Para habilitar a demonstração do modelo de uso, especifique a propriedade personalizada `RI_UsageModelDemo=true` no momento da embalagem. Se estiver empacotando conteúdo usando a ferramenta de linha de comando do Media Packager, especifique:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Se você não ativar o modo de demonstração opcional no momento do empacotamento, o servidor de licença usará a política especificada no momento do empacotamento para emitir uma licença. Se várias políticas tiverem sido especificadas, o servidor de licenças usará a primeira política válida.

Na demonstração, a lógica de negócios no servidor controla os atributos reais das licenças geradas. No momento do empacotamento, somente as informações mínimas da política devem ser incluídas no conteúdo. Especificamente, a política só precisa indicar se a autenticação é necessária para acessar o conteúdo. Para ativar todos os quatro modelos de uso, inclua uma política que permita acesso anônimo (para o modelo financiado por anúncio) e uma política que exija autenticação de nome de usuário/senha (para os outros três modelos de uso). Ao solicitar uma licença, um aplicativo cliente pode determinar se o usuário deve ser solicitado a fazer a autenticação com base nas informações de autenticação nas políticas.

Para controlar o modelo de uso sob o qual um usuário específico deve receber uma licença, podem ser adicionadas entradas no banco de dados de Implementação de referência. A variável `Customer` A tabela contém nomes de usuário e senhas para autenticar usuários. Também indica se o usuário tem uma assinatura. Os usuários com assinaturas receberão licenças sob a *Inscrição* modelo de uso. Para conceder acesso a um usuário sob o *Baixar para Próprio* ou *Vídeo sob demanda* modelos de uso, uma entrada pode ser adicionada à variável `CustomerAuthorization` tabela, que especifica cada parte do conteúdo que o usuário tem permissão para acessar e o modelo de uso. Consulte a [!DNL PopulateSampleDB.sql] script para obter detalhes sobre como preencher cada tabela.

Quando um usuário solicita uma licença, o servidor de implementação de referência verifica os metadados enviados pelo cliente para determinar se o conteúdo foi empacotado usando o `RI_UsageModelDemo` propriedade. Nesse caso, as seguintes regras de negócios serão usadas:

* Se uma das políticas exigir autenticação:

   * Se a solicitação tiver um token de autenticação válido, procure o usuário na tabela de banco de dados Cliente. Se o usuário foi encontrado:

      * Se a variável `Customer.IsSubscriber` propriedade é `true`, gere uma licença para o *Inscrição* modelo de uso e envie-o para o usuário.

      * Procure um registro na variável `CustomerAuthorization` tabela do banco de dados para este usuário e ID de conteúdo. Se um registro foi encontrado:

         * Se `CustomerAuthorization.UsageType` é `DTO`, gere uma licença para o *Baixar para Próprio* modelo de uso e envie-o para o usuário.

         * Se `CustomerAuthorization.UsageType` é `VOD`, gere uma licença para o *Vídeo sob demanda* modelo de uso e envie-o para o usuário.
   * Se nenhuma das políticas permitir acesso anônimo:

      * Se não houver um token de autenticação válido na solicitação, retorne um erro &quot;autenticação necessária&quot;.
      * Caso contrário, retorne um erro &quot;não autorizado&quot;.


* Se uma das políticas permitir acesso anônimo, gere uma licença para o modelo de uso financiado por anúncio e envie-a para o usuário.

Antes do servidor de Implementação de referência poder emitir licenças para a demonstração do modelo de uso, o servidor precisa ser configurado para especificar como as licenças são geradas para cada um dos quatro modelos de uso. Isso é feito especificando uma política para cada modelo de uso. A implementação de referência inclui quatro exemplos de políticas ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) ou você poderá substituir suas próprias políticas. Entrada [!DNL flashaccess-refimpl.properties], defina as seguintes propriedades para especificar a política a ser usada para cada modelo de uso e coloque os arquivos de política no diretório especificado pelo `config.resourcesDirectory` propriedade:

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
