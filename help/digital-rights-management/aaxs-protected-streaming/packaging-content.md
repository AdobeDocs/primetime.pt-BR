---
title: Conteúdo do empacotamento
description: Conteúdo do empacotamento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo, o URL do servidor de licenças deve ser especificado. O URL do Adobe Access Server tem o formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Por exemplo, para o nome de host do servidor de licenças &quot;mylicencieserver.com&quot; que escuta na porta 8080 e um locatário chamado &quot;tenant1&quot;, o URL do servidor de licenças a ser especificado no momento da embalagem é:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se cada locatário usar um License Server e uma Credencial de Transporte diferentes, certifique-se de especificar o certificado correto do locatário no empacotador.

Para garantir que o servidor emita licenças somente para conteúdo empacotado por empacotadores conhecidos, inclua o certificado do empacotador na lista de permissões do empacotador do arquivo de configuração do locatário.
