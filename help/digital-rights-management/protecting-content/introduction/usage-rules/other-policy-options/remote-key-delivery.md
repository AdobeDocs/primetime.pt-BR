---
title: Entrega de chave iOS remota e local
description: Entrega de chave iOS remota e local
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Entrega de chave iOS remota e local {#remote-and-local-ios-key-delivery}

O Adobe Primetime oferece suporte às seguintes opções para entrega de chaves a clientes do iOS:

* **Remoto**  - Executa conforme especificado na especificação HTTP Live Streaming (HLS); o manifesto M3U8 especifica um caminho HTTPS que inclui uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando você especifica `Remote` na política de DRM do Primetime, o dispositivo cliente deve se conectar a um servidor HTTPS remoto para obter uma chave AES.

* **Local**  - Ao especificar  `Local` no DRM do Primetime em vez de se conectar à Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo iOS, que gerencia todas as solicitações principais AES. O servidor HTTPS incorporado é automaticamente configurado e configurado no aplicativo P. O desenvolvedor de aplicativos não requer nenhuma intervenção.

A entrega de chave remota é ativada por meio da política DRM do Primetime usada para empacotar conteúdo. Se quiser alterar essa configuração, é necessário reempacotar o conteúdo. Se você habilitar a entrega remota de chaves, deverá implantar um Servidor de chaves DRM Primetime que possa gerenciar as principais solicitações dos clientes do iOS. No entanto, não há alterações no fluxo de trabalho de clientes em outras plataformas.

>[!NOTE]
>
>A seleção de delivery de chave afeta apenas os clientes do iOS. Todos os outros dispositivos que usam conteúdo HLS , como Android e Primetime on Desktop (Flash Player), sempre usam a entrega de chaves `Local`, mesmo que `Remote` tenha sido especificado.

