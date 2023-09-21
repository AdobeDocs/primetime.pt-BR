---
description: Ao criar o pacote de conteúdo, você deve especificar a URL do servidor de licenças.
title: Conteúdo de empacotamento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
