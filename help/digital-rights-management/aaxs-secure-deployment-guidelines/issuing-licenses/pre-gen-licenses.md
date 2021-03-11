---
title: Licenças pré-geradoras
description: Licenças pré-geradoras
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Licenças pré-geradoras{#pre-generating-licenses}

Se você estiver pré-gerando licenças que contêm regras de uso baseadas em tempo, é altamente recomendável que a licença inclua requisitos de sincronização (consulte *Usar o SDK de acesso do Adobe para proteger o conteúdo* guia), para que a expiração da licença possa ser imposta com segurança. A implementação de um mecanismo de &quot;pulsação&quot; entre o cliente e o servidor é altamente recomendável se você tiver restrições baseadas em tempo na licença, já que a pulsação sincronizará o horário do cliente com o horário do servidor.
