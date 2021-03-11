---
description: O TVSDK do navegador suporta atualmente a reprodução de fluxos em que manifestos e fragmentos não contêm extensões.
title: Fluxos sem extensão
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Fluxos sem extensão{#extensionless-streams}

O TVSDK do navegador suporta atualmente a reprodução de fluxos em que manifestos e fragmentos não contêm extensões.

## Nível do fragmento {#section_0E035129501D4A77BBC14192D8A53A86}

O TVSDK do navegador analisa os primeiros bytes da resposta para detectar o tipo de conteúdo de fragmentos sem extensão. Se nenhum tipo de conteúdo válido for detectado, o TVSDK do navegador emitirá um erro.

## Nível de manifesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

O TVSDK do navegador usa o parâmetro `mediaResource.resourceType` passado no método `replaceCurrentResource` para detectar o tipo de conteúdo do URL de manifesto. Para obter mais informações, consulte a classe `AdobePSDK.MediaPlayer` .

No reprodutor da Estrutura da interface do usuário, é possível especificar o tipo de recurso no recurso de mídia da seguinte maneira:

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

Se `resourceType` não for fornecido, a Estrutura da interface do usuário determinará o tipo de recurso da extensão do URL do recurso, que será passado para o método `replaceCurrentResource`.

>[!TIP]
>
>Para manifesto sem extensão, verifique se `resourceType` é sempre passado ao carregar um recurso na Estrutura da interface do usuário.

