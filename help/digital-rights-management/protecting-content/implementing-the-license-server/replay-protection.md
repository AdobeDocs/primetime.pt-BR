---
title: Proteção contra repetição
description: Proteção contra repetição
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Proteção contra repetição{#replay-protection}

Para proteção contra repetição, verifique se o identificador de mensagem foi visto recentemente, chamando `RequestMessageBase.getMessageId()`. Nesse caso, um invasor pode estar tentando repetir a solicitação, que deve ser negada. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de IDs de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar o tempo que os identificadores de mensagem precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que carregue um carimbo de data e hora por mais do que o número especificado de segundos fora do horário do servidor.
