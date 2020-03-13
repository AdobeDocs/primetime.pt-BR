---
description: Você pode gerar tokens Expressplay para o conteúdo criptografado enviando solicitações de token para o servidor de token Expressplay apropriado.
seo-description: Você pode gerar tokens Expressplay para o conteúdo criptografado enviando solicitações de token para o servidor de token Expressplay apropriado.
seo-title: Tokens de apresentação
title: Tokens de apresentação
uuid: 6103e1b2-127d-4758-a589-15f0f3c73db1
translation-type: tm+mt
source-git-commit: d0ba1f98b16f6350ae842ca2ce1261bf49dd8a66

---


# Tokens de apresentação {#expressplay-tokens}

Você pode gerar tokens Expressplay para o conteúdo criptografado enviando solicitações de token para o servidor de token Expressplay apropriado.

Um exemplo é o seguinte URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

A ID de armazenamento da chave de criptografia de conteúdo ou CEKSID fornecida ao `kid` parâmetro e a chave de criptografia de conteúdo ou CEK fornecida ao `contentKey` parâmetro devem corresponder à ID de armazenamento da chave de criptografia de conteúdo e à chave de criptografia de conteúdo usada para empacotamento. O texto a seguir é um exemplo da resposta do servidor de token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

Você pode

* use o URL e a consulta retornados como URL do servidor de licenças, ou
* retire a consulta do URL e passe o ExpressPlayToken separadamente como um cabeçalho HTTP POST