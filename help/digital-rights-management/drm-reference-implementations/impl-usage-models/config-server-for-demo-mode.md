---
description: nulo
seo-description: nulo
seo-title: Configurar o modo de demonstração do modelo de uso
title: Configurar o modo de demonstração do modelo de uso
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurar o modo de demonstração do modelo de uso{#configure-usage-model-demo-mode}

Antes que o servidor de Implementação de referência possa emitir licenças para a demonstração do modelo de uso, você deve configurar o servidor para especificar como as licenças são geradas para cada um dos quatro modelos de uso. Isso significa que você precisa especificar uma política de DRM para cada modelo de uso. A Implementação de referência inclui as seguintes políticas de DRM de exemplo no [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] diretório:

* `dto-policy.pol` - (Download por conta própria)
* `vod-policy.pol` - (Aluguer/Vídeo sob demanda)
* `sub-policy.pol` - (Assinatura)
* `ad-policy.pol` - (Financiamento de anúncios)

>[!NOTE]
>
>É possível substituir essas políticas de amostra por suas próprias políticas de DRM.

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

1. Copie seus arquivos de política de amostra para o diretório especificado na `config.resourcesDirectory` propriedade em [!DNL flashaccess-refimpl.properties].
