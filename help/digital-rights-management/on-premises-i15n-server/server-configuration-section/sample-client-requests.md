---
title: Solicitações de Cliente de Exemplo
description: Solicitações de Cliente de Exemplo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Solicitações de Cliente de Exemplo{#sample-client-requests}

Você pode coletar uma biblioteca de solicitações de cliente de amostra usando ferramentas como o Charles Proxy ou o Wireshark. Você deve capturar as solicitações do cliente depois que o servidor de Individualização for configurado, usando a credencial de Transporte de Individualização. É possível enviar essas solicitações do cliente (via *curl* ou outra ferramenta) ao endpoint do Servidor de individualização para verificar se o servidor está funcionando corretamente. Por exemplo:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Você também pode enviar essas solicitações novamente após qualquer alteração na configuração do servidor ou atualizações da ECI/CRL.

Você também deve atualizar a página Estatísticas de individualização apropriadamente com transações de individualização bem-sucedidas.
