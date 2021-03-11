---
description: A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.
title: Otimização de redirecionamento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# Otimização de redirecionamento HTTP 302{#http-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de 302 respostas de redirecionamento, o que permite que o aplicativo balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver ativada no reprodutor, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas adicionais 302.

Esse recurso é desativado por padrão e você pode alterar essa configuração.

Se você habilitar esse recurso, ele funcionará corretamente somente se *todas* das seguintes condições forem verdadeiras; caso contrário, nenhuma otimização de redirecionamento ocorrerá e 302 respostas continuarão ocorrendo:

* Seu aplicativo foi compilado para o Adobe Flash Player 11.8, usando `-swf-version` 21 ou superior.
* Seus usuários finais têm o Adobe Flash Player 11.8 ou posterior instalado.

>[!IMPORTANT]
>
>Para garantir que os cookies sejam transmitidos com solicitações de anúncios, desative o redirecionamento 302. Quando o redirecionamento 302 é ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio do qual o cookie foi originado.

## Desative ou ative a otimização de redirecionamento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Use a propriedade `useRedirectedUrl` para ativar ou desativar o redirecionamento 302 (true).

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

