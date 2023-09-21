---
description: A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.
title: Otimização de redirecionamento HTTP 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Otimização de redirecionamento HTTP 302{#http-redirect-optimization}

A otimização de redirecionamento 302 minimiza o número de respostas de redirecionamento 302, o que permite que seu aplicativo faça o balanceamento de carga com mais eficiência.

Se uma solicitação de manifesto principal for redirecionada e a otimização 302 estiver habilitada no player, as solicitações subsequentes feitas para ativos desse manifesto usarão o local de domínio final, o que evita respostas 302 adicionais.

Esse recurso está desativado por padrão e você pode alterar essa configuração.

Se você habilitar esse recurso, ele funcionará corretamente somente se *all* Uma das seguintes condições é verdadeira; caso contrário, nenhuma otimização de redirecionamento ocorrerá e 302 respostas continuarão a ocorrer:

* Seu aplicativo foi compilado para o Flash Player Adobe 11.8, usando `-swf-version` 21 ou superior.
* Seus usuários finais têm o Adobe Flash Player 11.8 ou mais recente instalado.

>[!IMPORTANT]
>
>Para garantir que os cookies sejam passados com solicitações de anúncio, desabilite o redirecionamento 302. Quando o redirecionamento 302 está ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio que originou o cookie.

## Desabilitar ou habilitar otimização de redirecionamento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Use o `useRedirectedUrl` para ativar (true) ou desativar (false) o redirecionamento 302.

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
