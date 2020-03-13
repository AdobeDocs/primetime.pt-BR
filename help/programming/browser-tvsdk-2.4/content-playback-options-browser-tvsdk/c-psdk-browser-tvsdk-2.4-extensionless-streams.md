---
description: O TVSDK do navegador suporta atualmente a reprodução de fluxos nos quais manifestos e fragmentos não contêm extensões.
seo-description: O TVSDK do navegador suporta atualmente a reprodução de fluxos nos quais manifestos e fragmentos não contêm extensões.
seo-title: Fluxos sem extensão
title: Fluxos sem extensão
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Fluxos sem extensão{#extensionless-streams}

O TVSDK do navegador suporta atualmente a reprodução de fluxos nos quais manifestos e fragmentos não contêm extensões.

## Nível de fragmento {#section_0E035129501D4A77BBC14192D8A53A86}

O TVSDK do navegador analisa os primeiros bytes da resposta para detectar o tipo de conteúdo de fragmentos sem extensão. Se nenhum tipo de conteúdo válido for detectado, o TVSDK do navegador emitirá um erro.

## Nível do manifesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

O TVSDK do navegador usa o `mediaResource.resourceType` parâmetro passado no `replaceCurrentResource` método para detectar o tipo de conteúdo do URL manifest. Para obter mais informações, consulte a `AdobePSDK.MediaPlayer` classe.

No player da UI Framework, você pode especificar o tipo de recurso no recurso de mídia da seguinte forma:

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

Se não `resourceType` for fornecido, a Estrutura da interface do usuário determinará o tipo de recurso da extensão do URL do recurso, que é então passada para o `replaceCurrentResource` método.

>[!TIP]
>
>Para o manifesto sem extensão, verifique se `resourceType` é sempre passado ao carregar um recurso na Estrutura da interface do usuário.

