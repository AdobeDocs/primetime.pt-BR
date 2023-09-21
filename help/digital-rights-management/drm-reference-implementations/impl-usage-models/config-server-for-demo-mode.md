---
title: Configurar modo de demonstração do modelo de uso
description: Configurar modo de demonstração do modelo de uso
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Configurar modo de demonstração do modelo de uso{#configure-usage-model-demo-mode}

Antes do servidor de Implementação de referência poder emitir licenças para a demonstração do modelo de uso, você deve configurar o servidor para especificar como as licenças são geradas para cada um dos quatro modelos de uso. Isso significa que é necessário especificar uma política de DRM para cada modelo de uso. A Implementação de referência inclui os seguintes exemplos de políticas de DRM na [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] diretório:

* `dto-policy.pol` - (Download Por Conta Própria)
* `vod-policy.pol` - (Aluguel/Vídeo Sob Demanda)
* `sub-policy.pol` - (Assinatura)
* `ad-policy.pol` - (Financiado por anúncio)

>[!NOTE]
>
>É possível substituir essas políticas de exemplo pelas suas próprias políticas de DRM.

1. Definir essas propriedades em [!DNL flashaccess-refimpl.properties] para especificar a política de DRM que você planeja aplicar a cada modelo de uso:

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

1. Copie seus arquivos de política de amostra para o diretório especificado na `config.resourcesDirectory` propriedade no [!DNL flashaccess-refimpl.properties].
