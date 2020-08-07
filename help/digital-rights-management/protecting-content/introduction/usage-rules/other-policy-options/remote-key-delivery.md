---
seo-title: Delivery de chaves iOS remotas e locais
title: Delivery de chaves iOS remotas e locais
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Delivery de chaves iOS remotas e locais {#remote-and-local-ios-key-delivery}

A Adobe Primetime oferece suporte às seguintes opções de delivery principal para clientes iOS:

* **Remoto** - Executa conforme especificado na especificação HTTP Live Streaming (HLS); o manifesto M3U8 especifica um caminho HTTPS que inclui uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando você especifica `Remote` a política do Primetime DRM, o dispositivo cliente deve se conectar a um servidor HTTPS remoto para obter uma chave AES.

* **Local** - ao especificar `Local` no DRM Primetime em vez de se conectar à Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo iOS, que gerencia todas as solicitações principais AES. O servidor HTTPS incorporado é automaticamente configurado e configurado no aplicativo P. Não é necessária nenhuma intervenção do desenvolvedor de aplicativos.

O delivery de chave remota é ativado por meio da política DRM Primetime usada para empacotar conteúdo. Se desejar alterar essa configuração, é necessário reempacotar o conteúdo. Se você ativar o delivery de chave remota, deverá implantar um Servidor de chave DRM Primetime que possa gerenciar solicitações de chave de clientes iOS. No entanto, não há alteração no fluxo de trabalho para clientes em outras plataformas.

>[!NOTE]
>
>A seleção do delivery principal afeta apenas os clientes iOS. Todos os outros dispositivos que usam conteúdo HLS, como Android e Primetime on Desktop (Flash Player), sempre usam o `Local` delivery principal, mesmo que `Remote` tenha sido especificado.

