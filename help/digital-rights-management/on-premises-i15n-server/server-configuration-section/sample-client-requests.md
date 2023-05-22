---
title: Solicitações de Cliente de Exemplo
description: Solicitações de Cliente de Exemplo
copied-description: true
exl-id: 2b6a1349-aafc-4222-9081-525662f62961
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
