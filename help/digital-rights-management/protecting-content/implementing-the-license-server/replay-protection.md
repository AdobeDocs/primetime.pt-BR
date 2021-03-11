---
title: Proteção contra repetição
description: Proteção contra repetição
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Reproduzir proteção{#replay-protection}

Para proteção de repetição, você pode verificar se o identificador de mensagem foi visto recentemente, chamando `RequestMessageBase.getMessageId()`. Em caso afirmativo, um atacante pode estar a tentar responder novamente ao pedido, o que deve ser negado. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de ids de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar a quantidade de tempo em que os identificadores de mensagem precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que tenha um carimbo de data e hora por mais do que o número especificado de segundos da hora do servidor.
