---
title: Entrega de chave remota e local do iOS
description: Entrega de chave remota e local do iOS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Entrega de chave remota e local do iOS{#remote-and-local-ios-key-delivery}

O Adobe Primetime oferece suporte a duas opções para entrega de chaves a clientes iOS:

* Remoto - Exatamente como especificado na especificação HLS, o manifesto M3U8 especifica um caminho HTTPS que contém uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando &quot;Remoto&quot; for especificado, o dispositivo cliente entrará em contato com um servidor HTTPS remoto para buscar a chave AES.
* Local - Quando &quot;Local&quot; é especificado, em vez de alcançar pela Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo do iOS que lidará com todas as solicitações de chave AES. O servidor HTTPS incorporado é automaticamente configurado no aplicativo Primetime. Nenhuma intervenção é necessária por parte do desenvolvedor de aplicativos.

A entrega de chave remota é habilitada por meio da política usada para empacotar conteúdo (a alteração dessa configuração requer o reempacotamento de conteúdo). Quando a entrega de chave remota é habilitada, um Servidor de Chave de Acesso ao Adobe deve ser implantado para lidar com solicitações de chave de clientes iOS, mas não há alteração no fluxo de trabalho para clientes em outras plataformas.

>[!NOTE]
>
>A seleção de Key delivery afeta apenas os clientes do iOS. Todos os outros dispositivos que consomem conteúdo HLS sempre usarão a entrega de chave &quot;Local&quot;, mesmo que &quot;Remoto&quot; tenha sido especificado.

Para obter informações, consulte *Uso do servidor da chave de acesso Adobe*.
