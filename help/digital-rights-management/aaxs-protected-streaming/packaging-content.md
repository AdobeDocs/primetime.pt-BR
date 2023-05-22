---
title: Conteúdo de empacotamento
description: Conteúdo de empacotamento
copied-description: true
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo, a URL do servidor de licenças deve ser especificada. O URL do Adobe Access Server tem o formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Por exemplo, para o nome de host do servidor de licença &quot;mylicenseserver.com&quot; que está escutando na porta 8080 e um locatário chamado &quot;tenant1&quot;, o URL do servidor de licença a ser especificado no momento do empacotamento é:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se cada locatário usar um License Server e uma credencial de transporte diferentes, especifique o certificado de locatário correto no empacotador.

Para garantir que o servidor emita licenças somente para conteúdo empacotado por empacotadores conhecidos, inclua o certificado do empacotador na lista de permissões do empacotador do arquivo de configuração do locatário.
