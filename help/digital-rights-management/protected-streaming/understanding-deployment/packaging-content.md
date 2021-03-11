---
description: Ao empacotar o conteúdo, você deve especificar o URL do servidor de licenças.
title: Conteúdo do empacotamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Conteúdo de empacotamento{#packaging-content}

Ao empacotar o conteúdo, você deve especificar o URL do servidor de licenças.

O URL do servidor DRM da Adobe Primetime usa o seguinte formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Por exemplo, para o nome de host do servidor de licenças `mylicenseserver.com` que escuta na porta 8080 e um locatário chamado *`tenant1`*, você usaria a seguinte sintaxe para o URL do servidor de licenças especificado no momento em que você empacotar o conteúdo:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se cada locatário usar um License Server e uma Credencial de Transporte diferentes, especifique o certificado correto do locatário no empacotador.

Se você quiser garantir que o servidor emita licenças somente para conteúdo de pacotes conhecidos, será necessário incluir o certificado do empacotador na lista de permissões do empacotador do arquivo de configuração do locatário.
