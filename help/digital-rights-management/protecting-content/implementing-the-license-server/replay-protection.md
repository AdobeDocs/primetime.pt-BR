---
seo-title: Proteção contra repetição
title: Proteção contra repetição
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Proteção contra repetição{#replay-protection}

Para obter proteção de reprodução, verifique se o identificador de mensagem foi visto recentemente, ligando para `RequestMessageBase.getMessageId()`. Em caso afirmativo, um atacante pode estar a tentar repetir o pedido, que deve ser negado. Para detectar tentativas de repetição, o servidor pode armazenar uma lista de IDs de mensagem vistas recentemente e verificar cada solicitação recebida na lista em cache. Para limitar a quantidade de tempo que os identificadores de mensagens precisam ser armazenados, chame `HandlerConfiguration.setTimestampTolerance()`. Se essa propriedade for definida, o SDK negará qualquer solicitação que tenha um carimbo de data e hora por mais do que o número especificado de segundos após o horário do servidor.
