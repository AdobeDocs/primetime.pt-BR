---
seo-title: Conteúdo de empacotamento
title: Conteúdo de empacotamento
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo para o delivery de chave remota, use uma política que especifique que o delivery de chave remota é necessário. O URL do servidor de chaves deve ser incluído no M3U8 (arquivo manifest) para o conteúdo HLS. O URL do servidor de chaves DRM Primetime tem o formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Por exemplo, para o nome de host do Key Server [!DNL mykeyserver.com] que está acompanhando na porta 443 e um locatário chamado `tenant1`, o URL do servidor de chaves a ser especificado no M3U8 é:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

O mesmo URL pode ser usado para clientes iOS e Xbox 360. Ou, se o servidor estiver configurado com locatários separados para cada tipo de cliente, URLs diferentes poderão ser usados.

O mesmo conteúdo pode ser reproduzido em clientes que não necessitam de um servidor de chaves, desde que o URL do servidor de licenças aponte para um servidor de licenças em execução corretamente configurado.
