---
title: Solicitações de cliente de exemplo
description: Solicitações de cliente de exemplo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Solicitações de exemplo do cliente{#sample-client-requests}

Você pode coletar uma biblioteca de solicitações de exemplo do cliente usando ferramentas como Charles Proxy ou Wireshark. Você deve capturar solicitações do cliente depois que o servidor de individualização tiver sido configurado, usando a credencial de Transporte de individualização. Em seguida, você pode enviar essas solicitações do cliente (via *curl* ou outra ferramenta) para o ponto final do Servidor de individualização para verificar se o servidor está funcionando corretamente. Por exemplo:

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

Também é possível enviar essas solicitações novamente depois de qualquer alteração na configuração do servidor ou de atualizações de ECI/CRL.

Você também deve atualizar a página Estatísticas de individualização apropriadamente com transações de individualização bem-sucedidas.
