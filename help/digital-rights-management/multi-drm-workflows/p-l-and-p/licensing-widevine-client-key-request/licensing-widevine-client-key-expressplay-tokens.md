---
description: Você pode gerar tokens de expressão para seu conteúdo criptografado enviando solicitações de token para o servidor de token de expressão adequado.
title: Exprimir tokens
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Apresentar tokens {#expressplay-tokens}

Você pode gerar tokens de expressão para seu conteúdo criptografado enviando solicitações de token para o servidor de token de expressão adequado.

Um exemplo é o seguinte URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

A ID de armazenamento da chave de criptografia de conteúdo ou CEKSID fornecida ao parâmetro `kid` e a chave de criptografia de conteúdo ou CEK fornecida ao parâmetro `contentKey` devem corresponder à ID de armazenamento da chave de criptografia de conteúdo e à chave de criptografia de conteúdo usada para empacotamento. O texto a seguir é um exemplo da resposta do servidor de token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

Você pode

* usar o URL retornado e a consulta como o URL do servidor de licença ou
* retire a consulta do URL e passe o ExpressPlayToken separadamente como um cabeçalho POST HTTP