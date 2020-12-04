---
description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-description: A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.
seo-title: Otimização de redirecionamento HTTP 302
title: Otimização de redirecionamento HTTP 302
uuid: 58593d5f-a639-4d87-9589-dba6b2dbba38
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Otimização de redirecionamento HTTP 302{#http-redirect-optimization}

A otimização do redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que o aplicativo balanceamento de carga seja mais eficiente.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita 302 respostas adicionais.

Esse recurso é desativado por padrão e você pode alterar essa configuração.

Se você ativar esse recurso, ele funcionará corretamente somente se *todas* das seguintes condições forem verdadeiras; caso contrário, nenhuma otimização de redirecionamento ocorrerá e 302 respostas continuarão ocorrendo:

* Seu aplicativo foi compilado para o Adobe Flash Player 11.8, usando `-swf-version` 21 ou superior.
* Seus usuários finais têm o Adobe Flash Player 11.8 ou posterior instalado.

>[!IMPORTANT]
>
>Para garantir que os cookies sejam enviados com solicitações de anúncio, desative o redirecionamento 302. Quando o redirecionamento 302 é ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio do qual o cookie se originou.

## Desabilitar ou habilitar a otimização de redirecionamento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Use a propriedade `useRedirectedUrl` para ativar o redirecionamento 302 (true) ou desativar (false).

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

Por exemplo:

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```

