---
seo-title: Delivery de chave iOS remota e local
title: Delivery de chave iOS remota e local
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Delivery de chave iOS remota e local{#remote-and-local-ios-key-delivery}

A Adobe Primetime oferece suporte a duas opções para o delivery principal para clientes iOS:

* Remoto - Exatamente como especificado na especificação HLS, o manifesto M3U8 especifica um caminho HTTPS que contém uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando &quot;Remoto&quot; for especificado, o dispositivo cliente chegará a um servidor HTTPS remoto para buscar a chave AES.
* Local - quando &quot;Local&quot; é especificado, em vez de alcançar pela Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo iOS que lidará com todas as solicitações de chave AES. O servidor HTTPS incorporado é automaticamente configurado e configurado no aplicativo Primetime. Não é necessária nenhuma intervenção do desenvolvedor de aplicativos.

O delivery de chave remota é habilitado por meio da política usada para disponibilizar conteúdo (a alteração dessa configuração requer o reempacotamento do conteúdo). Quando o delivery de chave remota é ativado, um Servidor de chave de acesso Adobe para lidar com as principais solicitações dos clientes iOS, mas não há alteração no fluxo de trabalho para clientes em outras plataformas.

>[!NOTE]
>
>A seleção do delivery principal afeta apenas os clientes iOS. Todos os outros dispositivos que consomem conteúdo HLS sempre usarão o delivery de chave &quot;Local&quot;, mesmo se &quot;Remoto&quot; tiver sido especificado.

Para obter informações, consulte *Usando o Servidor de Chaves de Acesso ao Adobe*.
