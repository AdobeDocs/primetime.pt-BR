---
title: Licenças pré-geradas
description: Licenças pré-geradas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Licenças pré-geradas{#pre-generating-licenses}

Se você estiver pré-gerando licenças que contêm regras de uso baseadas em tempo, é altamente recomendável que a licença inclua requisitos de sincronização (Consulte *Utilização do SDK do Adobe Access para proteção de conteúdo* guia), para que a expiração da licença possa ser imposta com segurança. A implementação de um mecanismo de &quot;pulsação&quot; entre o cliente e o servidor é altamente recomendada se você tiver restrições baseadas em tempo na licença, já que a pulsação sincronizará o tempo do cliente com o tempo do servidor.
