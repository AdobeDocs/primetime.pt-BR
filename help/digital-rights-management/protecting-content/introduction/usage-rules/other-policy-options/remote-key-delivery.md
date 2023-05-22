---
title: Entrega de chave remota e local do iOS
description: Entrega de chave remota e local do iOS
copied-description: true
exl-id: becc2d3f-39f3-40ee-b980-7dfbbe6f569d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Entrega de chave remota e local do iOS {#remote-and-local-ios-key-delivery}

A Adobe Primetime oferece suporte às seguintes opções para entrega de chaves a clientes iOS:

* **Remoto** - É executado conforme especificado na especificação HTTP Live Streaming (HLS); o manifesto M3U8 especifica um caminho HTTPS que inclui uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Ao especificar `Remote` na política DRM do Primetime, o dispositivo cliente deve se conectar a um servidor HTTPS remoto para obter uma chave AES.

* **Local** - Quando especificar `Local` no DRM do Primetime, em vez de se conectar à Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo do iOS, que gerencia todas as solicitações de chave AES. O servidor HTTPS incorporado é automaticamente configurado no aplicativo P. Nenhuma intervenção é necessária por parte do desenvolvedor de aplicativos.

A entrega da chave remota é habilitada por meio da política DRM do Primetime usada para empacotar conteúdo. Se quiser alterar essa configuração, reempacote o conteúdo. Se você habilitar a entrega remota de chaves, deverá implantar um Servidor de Chaves DRM do Primetime que possa gerenciar solicitações de chaves de clientes iOS. No entanto, não há alterações no workflow para clientes em outras plataformas.

>[!NOTE]
>
>A seleção de Key delivery afeta apenas os clientes do iOS. Todos os outros dispositivos que usam conteúdo HLS, como Android e Primetime on Desktop (Flash Player), sempre usam `Local` entrega de chaves, mesmo que `Remote` foi especificado.
