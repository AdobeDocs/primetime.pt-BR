---
description: Você pode gerar tokens Expressplay para o conteúdo criptografado enviando solicitações de token para o servidor de token Expressplay apropriado.
title: Tokens de expressão
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Tokens de expressão {#expressplay-tokens}

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

A ID de armazenamento da chave de criptografia de conteúdo ou CEKSID fornecida para o `kid` e a chave de criptografia de conteúdo ou CEK fornecida ao `contentKey` O parâmetro deve corresponder à ID de armazenamento da chave de criptografia de conteúdo e à chave de criptografia de conteúdo usadas para o empacotamento. O texto a seguir é um exemplo da resposta do servidor de token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

Você pode então:

* usar o URL retornado e consultar como o URL do servidor de licenças, ou
* retire a consulta do URL e passe o ExpressPlayToken separadamente como um cabeçalho de POST HTTP
