---
seo-title: Entrega de chaves iOS remotas e locais
title: Entrega de chaves iOS remotas e locais
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Entrega de chaves iOS remotas e locais{#remote-and-local-ios-key-delivery}

O Adobe Primetime oferece suporte a duas opções para a entrega de chaves a clientes iOS:

* Remoto - Exatamente como especificado na especificação HLS, o manifesto M3U8 especifica um caminho HTTPS que contém uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando &quot;Remoto&quot; for especificado, o dispositivo cliente chegará a um servidor HTTPS remoto para buscar a chave AES.
* Local - quando &quot;Local&quot; é especificado, em vez de alcançar pela Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo iOS que lidará com todas as solicitações de chave AES. O servidor HTTPS incorporado é automaticamente configurado e configurado no aplicativo Primetime. Não é necessária nenhuma intervenção do desenvolvedor de aplicativos.

A entrega da chave remota é ativada por meio da política usada para disponibilizar conteúdo (a alteração dessa configuração requer o reempacotamento do conteúdo). Quando a entrega da chave remota é ativada, um Servidor de Chave do Adobe Access deve ser implantado para lidar com as principais solicitações dos clientes do iOS, mas não há alteração no fluxo de trabalho para clientes em outras plataformas.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A seleção de entrega de chave afeta apenas os clientes iOS. Todos os outros dispositivos que consomem conteúdo HLS sempre usarão a entrega de chave &quot;Local&quot;, mesmo se &quot;Remoto&quot; tiver sido especificado.

Para obter informações, consulte *Uso do Adobe Access Key Server*.
