---
seo-title: Conteúdo de empacotamento
title: Conteúdo de empacotamento
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo, o URL do servidor de licenças deve ser especificado. O URL do Adobe Access Server tem o formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Por exemplo, para o nome do host do servidor de licenças &quot;mylicencieserver.com&quot; que escuta na porta 8080 e um locatário chamado &quot;locatário1&quot;, o URL do servidor de licenças a ser especificado no momento do empacotamento é:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se cada locatário usar um License Server e uma credencial de transporte diferentes, especifique o certificado correto do locatário no empacotador.

Para garantir que o servidor emita licenças somente para conteúdo empacotado por empacotadores conhecidos, inclua o certificado do empacotador na lista de permissões do empacotador do arquivo de configuração do locatário.
