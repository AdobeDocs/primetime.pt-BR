---
title: Configurar o modo de demonstração do modelo de uso
description: Configurar o modo de demonstração do modelo de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Configurar o modo de demonstração do modelo de uso{#configure-usage-model-demo-mode}

Antes que o servidor de Implementação de Referência possa emitir licenças para a demonstração do modelo de uso, você deve configurar o servidor para especificar como as licenças são geradas para cada um dos quatro modelos de uso. Isso significa que você precisa especificar uma política de DRM para cada modelo de uso. A Implementação de referência inclui as seguintes políticas de DRM de exemplo no diretório [!DNL Reference Implementation/Server/Reference Implementation Server/resources/]:

* `dto-policy.pol` - (Download Por Conta Própria)
* `vod-policy.pol` - (Aluguel/Vídeo sob Demanda)
* `sub-policy.pol` - (Assinatura)
* `ad-policy.pol` - (Financiamento de anúncios)

>[!NOTE]
>
>Você pode substituir essas políticas de exemplo por suas próprias políticas de DRM.

1. Defina essas propriedades em [!DNL flashaccess-refimpl.properties] para especificar a política de DRM que você planeja aplicar a cada modelo de uso:

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. Copie os arquivos de política de amostra para o diretório especificado na propriedade `config.resourcesDirectory` em [!DNL flashaccess-refimpl.properties].
