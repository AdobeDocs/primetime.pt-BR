---
title: Conteúdo do empacotamento
description: Conteúdo do empacotamento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo para entrega remota de chaves, use uma política que especifique que a entrega remota de chaves é necessária. O URL do Servidor de Chave deve ser incluído no M3U8 (arquivo de manifesto) para o conteúdo HLS. O URL do servidor de chaves DRM do Primetime tem o formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Por exemplo, para o nome de host do Servidor de Chave [!DNL mykeyserver.com] escutando na porta 443 e um locatário chamado `tenant1`, o URL do servidor de chaves a ser especificado no M3U8 é:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

O mesmo URL pode ser usado para clientes iOS e Xbox 360. Ou, se o servidor for configurado com locatários separados para cada tipo de cliente, URLs diferentes poderão ser usados.

O mesmo conteúdo pode ser reproduzido em clientes que não exigem um servidor de chaves, desde que o URL do servidor de licenças aponte para um servidor de licenças que esteja sendo configurado corretamente.
