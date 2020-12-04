---
description: Ao empacotar conteúdo, você deve especificar o URL do servidor de licenças.
seo-description: Ao empacotar conteúdo, você deve especificar o URL do servidor de licenças.
seo-title: Conteúdo de empacotamento
title: Conteúdo de empacotamento
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Conteúdo de empacotamento{#packaging-content}

Ao empacotar conteúdo, você deve especificar o URL do servidor de licenças.

O URL do servidor Adobe Primetime DRM usa o seguinte formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Por exemplo, para o nome do host do servidor de licenças `mylicenseserver.com` que escuta na porta 8080 e um locatário chamado *`tenant1`*, você usaria a seguinte sintaxe para o URL do servidor de licenças que você especificou no momento em que empacotou o conteúdo:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se cada locatário usar um License Server e uma credencial de transporte diferentes, certifique-se de especificar o certificado correto do locatário no empacotador.

Se você deseja certificar-se de que o servidor emite licenças somente para conteúdo de empacotadores conhecidos, é necessário incluir o certificado do empacotador na lista de permissões do empacotador do arquivo de configuração do locatário.
