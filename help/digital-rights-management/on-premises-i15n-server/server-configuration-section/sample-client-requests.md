---
seo-title: Amostra de solicitações do cliente
title: Amostra de solicitações do cliente
uuid: 330d5e3c-1711-4375-bd11-e7702f0cde31
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Amostra de solicitações do cliente{#sample-client-requests}

Você pode coletar uma biblioteca de solicitações de clientes de amostra usando ferramentas como Charles Proxy ou Wireshark. Você deve capturar as solicitações do cliente depois que o servidor de individualização for configurado, usando a credencial de Transporte de individualização. Em seguida, você pode enviar essas solicitações do cliente (via *curl* ou outra ferramenta) para o ponto final do servidor de personalização para verificar se o servidor está funcionando corretamente. Por exemplo:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Também é possível enviar essas solicitações novamente após qualquer alteração na configuração do servidor ou atualizações de ECI/CRL.

Você também deve atualizar a página Estatísticas de individualização apropriadamente com transações de individualização bem-sucedidas.
