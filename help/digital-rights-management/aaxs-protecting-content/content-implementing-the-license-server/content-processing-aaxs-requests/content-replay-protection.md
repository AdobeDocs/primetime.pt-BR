---
title: Proteção contra repetição
description: Proteção contra repetição
copied-description: true
exl-id: dfb6d615-07d2-4303-82cc-10cfee4bb387
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Proteção contra repetição{#replay-protection}

Para proteção contra repetição, pode ser prudente verificar se o identificador de mensagem foi visto recentemente, chamando `RequestMessageBase.getMessageId()`. Nesse caso, um invasor pode estar tentando repetir a solicitação, que deve ser negada. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de IDs de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar o tempo que os identificadores de mensagem precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que carregue um carimbo de data e hora maior do que o número especificado de segundos fora do horário do servidor.
