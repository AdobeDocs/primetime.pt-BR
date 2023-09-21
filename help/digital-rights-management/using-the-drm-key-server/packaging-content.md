---
title: Conteúdo de empacotamento
description: Conteúdo de empacotamento
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo para entrega de chave remota, use uma política que especifique que a entrega de chave remota é necessária. O URL do servidor de chaves deve ser incluído no M3U8 (arquivo de manifesto) para o conteúdo HLS. A URL do servidor de chaves DRM do Primetime tem o formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Por exemplo, para o nome de host do Servidor de Chaves [!DNL mykeyserver.com] escutando na porta 443 e um locatário chamado `tenant1`, o URL do servidor de chaves a ser especificado no M3U8 é:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

O mesmo URL pode ser usado para clientes iOS e Xbox 360. Ou, se o servidor estiver configurado com locatários separados para cada tipo de cliente, URLs diferentes poderão ser usados.

O mesmo conteúdo pode ser reproduzido em clientes que não exigem um servidor de chaves, desde que o URL do servidor de licenças aponte para um servidor de licenças em execução corretamente configurado.
