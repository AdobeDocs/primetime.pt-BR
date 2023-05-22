---
title: Licenças pré-geradas
description: Licenças pré-geradas
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Licenças pré-geradas{#pre-generating-licenses}

Se você estiver pré-gerando licenças que contêm regras de uso baseadas em tempo, é altamente recomendável que a licença inclua requisitos de sincronização (Consulte *Utilização do SDK do Adobe Access para proteção de conteúdo* guia), para que a expiração da licença possa ser imposta com segurança. A implementação de um mecanismo de &quot;pulsação&quot; entre o cliente e o servidor é altamente recomendada se você tiver restrições baseadas em tempo na licença, já que a pulsação sincronizará o tempo do cliente com o tempo do servidor.
