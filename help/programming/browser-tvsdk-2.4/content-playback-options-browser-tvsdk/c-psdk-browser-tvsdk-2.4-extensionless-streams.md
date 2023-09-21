---
description: Atualmente, o TVSDK do navegador é compatível com a reprodução de fluxos em que manifestos e fragmentos não contêm extensões.
title: Fluxos sem extensão
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Fluxos sem extensão{#extensionless-streams}

Atualmente, o TVSDK do navegador é compatível com a reprodução de fluxos em que manifestos e fragmentos não contêm extensões.

## Nível do fragmento {#section_0E035129501D4A77BBC14192D8A53A86}

O TVSDK do navegador analisa os primeiros bytes da resposta para detectar o tipo de conteúdo de fragmentos sem extensão. Se nenhum tipo de conteúdo válido for detectado, o TVSDK do navegador exibirá um erro.

## Nível do manifesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

O TVSDK do navegador usa o `mediaResource.resourceType` parâmetro passado na variável `replaceCurrentResource` para detectar o tipo de conteúdo do URL do manifesto. Para obter mais informações, consulte `AdobePSDK.MediaPlayer` classe.

No reprodutor da estrutura da interface do usuário, você pode especificar o tipo de recurso no recurso de mídia da seguinte maneira:

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

Se `resourceType` não for fornecido, a Estrutura da interface determina o tipo de recurso da extensão de URL de recurso, que é então passada para `replaceCurrentResource` método.

>[!TIP]
>
>Para manifesto sem extensão, verifique se `resourceType` é sempre transmitido ao carregar um recurso na Estrutura da interface do usuário.
