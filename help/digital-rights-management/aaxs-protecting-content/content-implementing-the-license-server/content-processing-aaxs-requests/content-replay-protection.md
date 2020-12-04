---
seo-title: Proteção contra repetição
title: Proteção contra repetição
uuid: 75f2be65-b2fc-428a-b853-34a4b30960ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Reproduzir proteção{#replay-protection}

Para a proteção de repetição, pode ser prudente verificar se o identificador de mensagem foi visto recentemente ao chamar `RequestMessageBase.getMessageId()`. Em caso afirmativo, um atacante pode estar a tentar repetir o pedido, que deve ser negado. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de IDs de mensagem vistas recentemente e verificar cada solicitação recebida em relação à lista em cache. Para limitar a quantidade de tempo que os identificadores de mensagens precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que tenha um carimbo de data e hora maior que o número especificado de segundos após o horário do servidor.
