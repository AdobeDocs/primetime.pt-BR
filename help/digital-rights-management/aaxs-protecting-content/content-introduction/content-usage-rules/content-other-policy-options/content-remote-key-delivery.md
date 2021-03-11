---
title: Entrega de chaves iOS remotas e locais
description: Entrega de chaves iOS remotas e locais
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Entrega de chave iOS remota e local{#remote-and-local-ios-key-delivery}

O Adobe Primetime oferece suporte a duas opções para entrega de chaves a clientes do iOS:

* Remoto - Exatamente como especificado na especificação HLS, o manifesto M3U8 especifica um caminho HTTPS que contém uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando &quot;Remoto&quot; for especificado, o dispositivo cliente chegará a um servidor HTTPS remoto para buscar a chave AES.
* Local - Quando &quot;Local&quot; é especificado, em vez de alcançar pela Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo iOS que lidará com todas as solicitações de chave AES. O servidor HTTPS incorporado é automaticamente configurado e configurado no aplicativo Primetime. O desenvolvedor de aplicativos não requer nenhuma intervenção.

A entrega de chave remota é ativada por meio da política usada para empacotar conteúdo (a alteração dessa configuração requer o reempacotamento de conteúdo). Quando a entrega de chave remota é habilitada, um Servidor de Chave de Acesso do Adobe deve ser implantado para lidar com solicitações de chave de clientes do iOS, mas não há alteração no fluxo de trabalho para clientes em outras plataformas.

>[!NOTE]
>
>A seleção de delivery de chave afeta apenas os clientes do iOS. Todos os outros dispositivos que consomem conteúdo HLS sempre usarão a entrega de chave &quot;Local&quot;, mesmo que &quot;Remoto&quot; tenha sido especificado.

Para obter informações, consulte *Usando o Servidor de Chave de Acesso do Adobe*.
