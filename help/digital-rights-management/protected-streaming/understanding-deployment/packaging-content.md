---
description: Ao criar o pacote de conteúdo, você deve especificar a URL do servidor de licenças.
title: Conteúdo de empacotamento
exl-id: f82385d5-cdb3-4c24-822e-3fc3c3a0793f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Conteúdo de empacotamento{#packaging-content}

Ao criar o pacote de conteúdo, você deve especificar a URL do servidor de licenças.

O URL do servidor DRM da Adobe Primetime usa o seguinte formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Por exemplo, para o nome de host do servidor de licenças `mylicenseserver.com` que escuta na porta 8080 e um locatário chamado *`tenant1`*, você usaria a seguinte sintaxe para o URL do servidor de licença especificado no momento em que você empacota o conteúdo:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se cada locatário usar um License Server e uma credencial de transporte diferentes, especifique o certificado de locatário correto no empacotador.

Se quiser garantir que o servidor emita licenças somente para conteúdo de empacotadores conhecidos, será necessário incluir o certificado do empacotador na lista de permissões do empacotador do arquivo de configuração do locatário.
