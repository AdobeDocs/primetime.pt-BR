---
seo-title: Entrega remota e local de chaves iOS
title: Entrega remota e local de chaves iOS
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Entrega remota e local de chaves iOS {#remote-and-local-ios-key-delivery}

O Adobe Primetime oferece suporte às seguintes opções para a entrega de chaves a clientes iOS:

* **Remoto** - Executa conforme especificado na especificação HTTP Live Streaming (HLS); o manifesto M3U8 especifica um caminho HTTPS que inclui uma chave AES que deve ser usada para descriptografar os seguintes segmentos criptografados no fluxo. Quando você especifica `Remote` a política do Primetime DRM, o dispositivo cliente deve se conectar a um servidor HTTPS remoto para obter uma chave AES.

* **Local** - ao especificar `Local` no DRM Primetime em vez de se conectar à Internet/rede para a chave AES, um servidor HTTPS local é incorporado ao aplicativo iOS, que gerencia todas as solicitações principais AES. O servidor HTTPS incorporado é automaticamente configurado e configurado no aplicativo P. Não é necessária nenhuma intervenção do desenvolvedor de aplicativos.

A entrega de chave remota é ativada por meio da política DRM Primetime usada para disponibilizar conteúdo. Se desejar alterar essa configuração, é necessário reempacotar o conteúdo. Se você ativar a entrega de chave remota, deverá implantar um Servidor de Chave DRM Primetime que possa gerenciar as principais solicitações dos clientes iOS. No entanto, não há alteração no fluxo de trabalho para clientes em outras plataformas.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A seleção de entrega de chave afeta apenas os clientes iOS. Todos os outros dispositivos que usam conteúdo HLS, como Android e Primetime on Desktop (Flash Player), sempre usam a entrega de `Local` chave, mesmo que `Remote` tenha sido especificada.

